<template>
  <section
    id="#weather-information"
    class="weather-results"
    v-if="typeof weather.main !== 'undefined'"
  >
    <div class="box information">
      <div class="temperature">
        <p>{{ Math.round(weather.main.temp) }}°c</p>
        <span>{{ weather.weather[0].main }}</span>
      </div>
      <div class="date">{{ datetime }}</div>
    </div>
    <div class="box details">
      <div class="city">{{ weather.name }}, {{ weather.sys.country }}</div>
      <div class="condition">{{ weather.weather[0].description }}</div>
    </div>
  </section>
</template>

<script>
export default {
  name: "WeatherInformation",
  props: ["weather", "datetime"],
};
</script>

<style lang="scss" scoped>
.box {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  width: 100%;
  height: 175px;
  padding: 32px 0;
  color: var(--color-white);
}
.weather-results {
  display: flex;
  height: 100%;
  flex-direction: column;
  justify-content: space-between;
  align-items: center;
  padding: 32px 0;
}

.information {
  background-color: rgba(0, 0, 0, 0.7);
  border-radius: var(--border-r-1);

  .temperature {
    display: flex;
    justify-content: center;
    align-items: flex-end;
    p {
      font-size: 3rem;
      margin-right: 8px;
    }
    span {
      color: rgba(255, 255, 255, 0.75);
    }
  }

  .date {
    margin-top: 16px;
  }
}

.details {
  .city {
    font-size: 3rem;
  }
  .condition {
    text-transform: capitalize;
    color: rgba(255, 255, 255, 0.75);
  }
}
</style>
