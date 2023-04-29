<template>
  <base-card :isActivated="isDataRecieved">
    <header><i class="bx bx-left-arrow-alt"></i>Weather App</header>
    <the-input @submit-data="submitData" :type="type"></the-input>
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
      type: "",
    };
  },
  watch: {
    cityName(newVal) {
      const theUrl = `https://api.weatherapi.com/v1/current.json?key=${this.key}&q=${newVal}&aqi=no`;
      this.type = "pending";
      fetch(theUrl, {
        method: "GET",
      })
        .then((response) => {
          if (response.ok) {
            return response.json();
          } else {
            this.type = "error";
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
          console.log(current);
        })
        .catch((err) => (this.type = "error"));
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
