<template>
  <div
    id="app"
    :class="[
      { warm: typeof weather.main !== 'undefined' && weather.main.temp > 16 },
      { cold: typeof weather.main !== 'undefined' && weather.main.temp < 16 },
    ]"
  >
    <main>
      <WeatherForm v-on:handle-search="fetchWeather" />
      <WeatherInformation :weather="weather" :datetime="datetime" />
    </main>
  </div>
</template>

<script>
import dayjs from "dayjs";

import WeatherInformation from "./components/WeatherInformation";
import WeatherForm from "./components/WeatherForm";

export default {
  name: "App",
  components: {
    WeatherInformation,
    WeatherForm,
  },
  data() {
    return {
      weather: {},
    };
  },
  methods: {
    fetchWeather(location, unit) {
      const fetchUrl = `${process.env.VUE_APP_API_BASE_URL}weather?q=${location}&units=${unit}&APPID=${process.env.VUE_APP_API_KEY}`;
      fetch(fetchUrl)
        .then(res => res.json())
        .then(data => {
          this.weather = data;
        });
    },
  },
  computed: {
    datetime: function() {
      return dayjs()
        .add(this.weather.timezone, "second")
        .format("dddd DD MMM YYYY");
    },
  },
};
</script>

<style lang="scss">
#app {
  width: 100vw;
  height: 100vh;
  overflow: hidden;
  background-image: url(./assets/images/bg.svg);
  background-size: 350% 100%;
  background-position: center;
  background-repeat: no-repeat;
  transition: 0.5s all ease-in-out;
}

#app.warm {
  background-image: url(./assets/images/bg_day.svg);
  background-position: center center;
}

#app.cold {
  background-image: url(./assets/images/bg_night.svg);
  background-position: center center;
}

main {
  width: 100%;
  height: 100vh;
  background-image: linear-gradient(to bottom, rgba(0, 0, 0, 0), rgba(0, 0, 0, 0.5));
  padding: 16px;
  display: flex;
  flex-direction: column;
}
</style>
