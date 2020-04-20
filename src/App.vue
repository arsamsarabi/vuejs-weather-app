<template>
  <div
    id="app"
    :class="typeof weather.main !== 'undefined' ? (weather.main.temp > 16 ? 'warm' : 'cold') : ''"
  >
    <main>
      <div class="search-box">
        <input
          type="text"
          placeholder="Search..."
          class="input-field"
          v-model="location"
          @keyup.enter="fetchWeather"
        />
      </div>

      <WeatherInformation :weather="weather" :datetime="datetime" />
    </main>
  </div>
</template>

<script>
import dayjs from 'dayjs'

import WeatherInformation from './components/WeatherInformation'

export default {
  name: 'App',
  components: {
    WeatherInformation,
  },
  data() {
    return {
      location: '',
      unit: 'metric',
      datetime: '',
      weather: {},
    }
  },
  methods: {
    fetchWeather() {
      const fetchUrl = `${process.env.VUE_APP_API_BASE_URL}weather?q=${this.location}&units=${this.unit}&APPID=${process.env.VUE_APP_API_KEY}`
      fetch(fetchUrl)
        .then(res => res.json())
        .then(this.handleResult)
    },
    handleResult(weather) {
      this.weather = weather
      this.dateBuilder()
    },
    dateBuilder() {
      this.datetime = dayjs()
        .add(this.weather.timezone, 'second')
        .format('DD MMM YYYY')
    },
  },
}
</script>

<style lang="scss">
#app {
  background-image: url(./assets/images/bg.svg);
  background-size: 350% 100%;
  background-position: -550px;
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
}

.input-field {
  width: 100%;
  height: 48px;
  border: none;
  outline: none;
  background: none;
  background-color: rgba(0, 0, 0, 0.25);
  padding: 8px 16px;
  font-size: 1.25rem;
  color: var(--color-white);
  border-radius: 8px 0 8px 0;
  transition: 0.4s all ease-out;

  &:focus,
  &:active {
    outline: none;
    background-color: rgba(0, 0, 0, 0.75);
    border-radius: 0 8px 0 8px;
  }
}

::placeholder {
  color: var(--color-white);
  opacity: 1;
}
</style>
