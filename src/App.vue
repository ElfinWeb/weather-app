<template>
  <base-card :isActivated="isDataRecieved">
    <header><i class="bx bx-left-arrow-alt"></i>Weather App</header>
    <the-input @submit-data="submitData"></the-input>
    <the-weather
      v-if="tempData"
      :tempData="tempData ? tempData : null"
      :isActivated="isDataRecieved"
    ></the-weather>
  </base-card>
</template>

<script>
import TheInput from "./components/TheInput.vue";
import TheWeather from "./components/TheWeather.vue";
export default {
  components: {
    TheInput,
    TheWeather,
  },
  data() {
    return {
      cityName: "",
      baseUrl: "https://api.weatherapi.com/v1/current.json",
      key: "e9fd98a95d4348ce8e9154823232804",
      tempData: null,
      isDataRecieved: false,
    };
  },
  watch: {
    cityName(newVal) {
      const theUrl = `https://api.weatherapi.com/v1/current.json?key=${this.key}&q=${newVal}&aqi=no`;
      fetch(theUrl, {
        method: "GET",
      })
        .then((response) => {
          if (response.ok) {
            return response.json();
          } else {
            throw new Error("There's something wrong");
          }
        })
        .then((data) => {
          const { location, current } = data;
          this.tempData = {
            location: location,
            current: current,
          };
          this.isDataRecieved = true;
        });
    },
  },
  methods: {
    submitData(inputValue) {
      this.cityName = inputValue;
    },
  },
};
</script>

<style scoped></style>
