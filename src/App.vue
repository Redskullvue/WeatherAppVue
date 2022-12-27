<template>
  <div>
    <div class="container">
      <div class="weather-info">
        <div>
          <i class="fa-solid fa-cloud weather-icon"></i>
          <i class="fa-solid fa-cloud-rain weather-icon"></i>
          <i class="fa-solid fa-sun weather-icon"></i>
        </div>
        <h1 style="text-align: center">Welcome To Weather App !</h1>
      </div>
      <div class="weather-details">
        <div v-if="weather.name" class="weather-city">
          <h3>{{ weather.name }}</h3>
          <div v-if="weather.name" class="temp">
            {{ Math.floor(weather.main.temp) - 273 }} C
          </div>
        </div>
        <ul v-if="weather.name" class="weather-stats">
          <li class="weather-items">Humidity : {{ weather.main.humidity }}</li>
          <li class="weather-items">
            Wind Speed : {{ weather.wind.speed }} Km/h
          </li>
          <li class="weather-items">State : {{ weather.weather[0].main }}</li>
        </ul>
      </div>
    </div>
    <div class="search-area">
      <input
        placeholder="Please Enter Your City"
        type="text"
        class="search-bar"
        v-model="userInput"
        @keypress="fetchData"
      />
    </div>
  </div>
</template>

<script>
import "./assets/css/index.css";
export default {
  name: "AppOne",
  data() {
    return {
      userInput: "",
      apiKey: "5a0b81ce3710f1170f8982606b79d1f8",
      api: "https://api.openweathermap.org/data/2.5/",
      weather: {},
    };
  },
  methods: {
    dateBuild() {
      let d = new Date();
      let monthes = [
        "Jan",
        "Feb",
        "March",
        "April",
        "May",
        "Jun",
        "Jul",
        "Aug",
        "Sep",
        "October",
        "Nov",
        "Dec",
      ];
      let days = ["Sun", "Mon", "Tue", "Wen", "Thu", "Fri", "Sat"];
      let day = days[d.getDay()];
      let date = d.getDate();
      let year = d.getFullYear();
      let month = monthes[d.getMonth()];

      return `${day}   ${date}  ${month}  ${year}`;
    },
    fetchData(event) {
      if (event.charCode == 13) {
        fetch(
          `${this.api}/weather?q=${this.userInput}&appid=${this.apiKey}`
        ).then((res) => {
          return res.json().then((response) => {
            this.weather = response;
          });
        });
      }
    },
    FetchBtn() {
      fetch(
        `${this.api}/weather?q=${this.userInput}&appid=${this.apiKey}`
      ).then((res) => {
        return res.json().then((response) => {
          this.weather = response;
        });
      });
    },
  },
};
</script>

<style>
* {
  font-family: serif;
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
</style>
