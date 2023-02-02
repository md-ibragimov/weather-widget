<template>
  <div :class="$style.container">
    <widget-header />
    <form @submit.prevent="handleWeather" :class="$style.form">
      <input
        :class="$style.search"
        placeholder="Введите название города"
        v-model="inputValue"
      />
      <button type="submit">Поиск</button>
    </form>
    <span v-if="status === 'load'">Загрузка...</span>
    <span v-else-if="status === 'error'">Некорректный запрос</span>
    <div v-else-if="status === 'success'" :class="$style.info">
      <div :class="$style.location">
        <span :class="$style.country">{{ data.location.country }}</span>
        <span :class="$style.city">{{ data.location.name }}</span>
      </div>
      <div :class="$style.value">Температура: {{ data.current.temp_c }} °С</div>
    </div>
  </div>
</template>

<script>
import WidgetHeader from "./WidgetHeader.vue";
import axios from "axios";
export default {
  components: { WidgetHeader },
  data() {
    return {
      inputValue: "",
      data: null,
      status: "waiting",
    };
  },
  methods: {
    handleWeather() {
      this.status = "load";
      axios
        .get(
          `https://api.weatherapi.com/v1/current.json?key=${import.meta.env.VITE_API_KEY}&q=${this.inputValue}&aqi=no`
        )
        .then((response) => {
          this.status = "success";
          this.data = response.data;
        })
        .catch(() => (this.status = "error"));
      this.inputValue = "";
    },
  },
};
</script>

<style module lang="scss">
.container {
  width: 100%;
  height: 100%;
  font-size: 16px;
  padding: 1em;
  display: flex;
  flex-direction: column;
  .form {
    width: 100%;
    height: 2em;
    display: flex;
    gap: 0.3em;
    .search {
      width: 100%;
      height: 100%;
      outline: none;
    }
  }
  .info {
    width: 100%;
    height: calc(100% - 5em);
    display: flex;
    flex-direction: column;
    gap: 2em;
    margin-top: 2em;
    .location {
      width: 100%;
      display: flex;
      align-items: center;
      gap: 1em;
      .country {
        font-size: 1.3em;
      }
    }
  }
}
</style>