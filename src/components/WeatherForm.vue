<template>
  <div class="search-box">
    <input
      type="text"
      placeholder="Search..."
      class="input-field"
      v-model="location"
      @keyup.enter="$emit('handle-search', location, unit)"
    />
  </div>
</template>

<script>
export default {
  name: 'WeatherForm',
  data() {
    return {
      location: '',
      unit: 'metric',
    }
  },
}
</script>

<style lang="scss" scoped>
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
