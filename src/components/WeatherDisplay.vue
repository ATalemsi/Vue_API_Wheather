<template>
  <div class="min-h-screen flex flex-col justify-between">
    <!-- Main content -->
    <div :class="weatherBackgroundClass" class="p-4 flex-1">
      <h2 class="text-2xl font-bold mb-4">Current Weather</h2>
      <div v-if="weatherData" class="mb-8">
        <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
          <!-- Current Weather Card -->
          <div
            class="bg-white rounded-lg shadow-md p-6 flex flex-col justify-center items-center"
          >
            <h3 class="text-lg font-semibold mb-4">Current Weather</h3>
            <div class="flex items-center mb-4">
              <img
                :src="weatherData.forecast.forecastday[0].day.condition.icon"
                alt="Weather Icon"
                class="w-16 h-16 mr-2"
              />
              <p class="text-3xl font-bold">
                {{ weatherData.forecast.forecastday[0].day.avgtemp_c }}°C
              </p>
            </div>
            <p class="text-lg">
              {{ weatherData.forecast.forecastday[0].day.condition.text }}
            </p>
            <p class="mt-4">
              <span class="font-semibold">City:</span>
              {{ weatherData.location.name }}
            </p>
            <p>
              <span class="font-semibold">Country:</span>
              {{ weatherData.location.country }}
            </p>
          </div>

          <!-- Short-Term Forecast Card -->
          <div class="bg-white rounded-lg shadow-md p-6">
            <h3 class="text-lg font-semibold mb-4">Short-Term Forecast</h3>
            <div v-if="shortTermForecast.length > 0">
              <div
                v-for="(hourlyForecast, index) in shortTermForecast"
                :key="index"
                class="mb-4"
              >
                <div class="flex items-center justify-between border-b pb-2">
                  <p class="text-base font-semibold">
                    {{ hourlyForecast.time }}
                  </p>
                  <div class="flex items-center">
                    <p class="text-lg font-semibold mr-2">
                      {{ hourlyForecast.temp_c }}°C
                    </p>
                    <img
                      :src="hourlyForecast.condition.icon"
                      alt="Weather Icon"
                      class="w-16 h-16"
                    />
                  </div>
                </div>
              </div>
            </div>
            <div v-else>
              <p class="italic">No short-term forecast available</p>
            </div>
          </div>
        </div>
      </div>
      <div v-else>
        <p class="italic">No weather data available</p>
      </div>
    </div>

    <!-- Search Input -->
    <div class="bg-white rounded-lg shadow-md p-4">
      <input
        type="text"
        placeholder="Search..."
        class="w-full px-4 py-2 border border-gray-300 rounded-lg focus:outline-none focus:border-blue-400"
      />
    </div>
  </div>
</template>

<script>
export default {
  props: {
    weatherData: Object,
  },
  computed: {
    shortTermForecast() {
      if (
        this.weatherData &&
        this.weatherData.forecast &&
        this.weatherData.forecast.forecastday.length > 0
      ) {
        return this.weatherData.forecast.forecastday[0].hour.slice(0, 3);
      }
      return [];
    },
    weatherBackgroundClass() {
      if (
        this.weatherData &&
        this.weatherData.forecast &&
        this.weatherData.forecast.forecastday.length > 0
      ) {
        const conditionCode =
          this.weatherData.forecast.forecastday[0].day.condition.code;
        switch (conditionCode) {
          case 1000:
            return "bg-gradient-to-b from-blue-100 to-blue-300";
          default:
            return "bg-gradient-to-b from-blue-100 to-blue-300";
        }
      }
      return "bg-gradient-to-b from-blue-100 to-blue-300";
    },
  },
};
</script>
