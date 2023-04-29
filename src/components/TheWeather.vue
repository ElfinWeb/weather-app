<template>
  <section class="weather-part">
    <img :src="iconLink" alt="Weather Icon" />
    <div class="temp">
      <span class="numb">{{ temp }}</span>
      <span class="deg">°</span>C
    </div>
    <div class="weather">{{ description }}</div>
    <div class="location">
      <i class="bx bx-map"></i>
      <span>{{ `${city}, ${country}` }}</span>
    </div>
    <div class="bottom-details">
      <div class="column feels">
        <i class="bx bxs-thermometer"></i>
        <div class="details">
          <div class="temp">
            <span class="numb-2">{{Math.floor(feelsLike)}}</span>
            <span class="deg">°</span>C
          </div>
          <p>Feels like</p>
        </div>
      </div>
      <div class="column humidity">
        <i class="bx bxs-droplet-half"></i>
        <div class="details">
          <span>{{ `${humidity}%` }}</span>
          <p>Humidity</p>
        </div>
      </div>
    </div>
  </section>
</template>

<script>
export default {
  props: ["tempData"],
  data() {
    return {
      cityData: this.tempData,
      temp: null,
      city: "",
      country: "",
      feelsLike: null,
      humidity: null,
      description: "",
      iconLink: ""
    };
  },
  created() {
    this.temp = this.cityData.current.temp_c;
    this.city = this.cityData.location.name;
    this.country = this.cityData.location.country;
    this.feelsLike = this.cityData.current.feelslike_c;
    this.humidity = this.cityData.current.humidity;
    this.description = this.cityData.current.condition.text;
    this.iconLink = this.cityData.current.condition.icon;
  },
};
</script>
