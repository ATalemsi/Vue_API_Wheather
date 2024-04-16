<template>
  <div class="mb-16">
    <form
      @submit.prevent="getWeather"
      class="flex items-center justify-center mt-8"
    >
      <input
        type="text"
        v-model="city"
        placeholder="Enter city name"
        class="border border-gray-300 rounded-md px-4 py-2 mr-2 focus:outline-none focus:border-blue-500"
      />
      <button
        type="submit"
        class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded"
      >
        Get Weather
      </button>
    </form>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data() {
    return {
      city: "casablanca",
    };
  },

  methods: {
    async getWeather() {
      try {
        const response = await axios.get(
          `https://api.weatherapi.com/v1/future.json?q=${this.city}&dt=2024-05-22&lang=1&key=bf892321b5ac473792e100947241604`
        );
        this.$emit("weather", response.data);
      } catch (error) {
        console.error("Error fetching weather data: ", error);
      }
    },
  },
};
</script>
