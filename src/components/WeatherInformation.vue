<template>
  <section
    id="#weather-information"
    class="weather-results"
    v-if="typeof weather.main !== 'undefined'"
  >
    <div class="location-details">
      <div class="city">{{ weather.name }}, {{ weather.sys.country }}</div>
      <div class="date">{{ datetime }}</div>
    </div>
    <div class="wheater-info">
      <div class="temperature">{{ Math.round(weather.main.temp) }}°c</div>
      <div class="condition">{{ weather.weather[0].main }}</div>
      <div class="condition-desc">{{ weather.weather[0].description }}</div>
    </div>
  </section>
</template>

<script>
export default {
  name: 'WeatherInformation',
  props: ['weather', 'datetime'],
}
</script>

<style lang="scss" scoped></style>
