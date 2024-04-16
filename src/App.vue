<template>
  <div id="app">
    <WeatherForm @weather="setWeatherData" />
    <WeatherDisplay :weatherData="weatherData" />
  </div>
</template>

<script>
import WeatherForm from "./components/WeatherForm.vue";
import WeatherDisplay from "./components/WeatherDisplay.vue";

export default {
  name: "App",
  components: {
    WeatherForm,
    WeatherDisplay,
  },
  data() {
    return {
      weatherData: null,
    };
  },
  methods: {
    setWeatherData(data) {
      this.weatherData = data;
    },
  },
};
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

nav {
  padding: 30px;

  a {
    font-weight: bold;
    color: #2c3e50;

    &.router-link-exact-active {
      color: #42b983;
    }
  }
}
</style>
