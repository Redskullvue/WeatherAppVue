<template>
  <div id="app">
    <main>
      <div class="search-box">
        <input
          v-model="userInput"
          type="text"
          class="search-bar"
          placeholder="Search... "
          @keypress="fetchData"
        />
        <br />
      </div>
      <div class="btnCont">
        <button class="btn" @click="FetchBtn">Check</button>
      </div>
      <h1 class="Error" v-if="weather.cod == 404">
        We Could not Find Your City
      </h1>
      <div class="container" v-if="typeof weather.main != 'undefined'">
        <div class="box">
          <div class="location-box">
            <div class="location">
              {{ weather.name }} , {{ weather.sys.country }}
            </div>
          </div>
          <div class="date">{{dateBuild()}}</div>
          <br />
          <div class="weather-box">
            <div class="temp">{{ Math.floor(weather.main.temp) - 273 }} C</div>
          </div>
          <div class="weather">
            <ul>
              <li>Humidity : {{ weather.main.humidity }}</li>
              <li>Wind Speed : {{ weather.wind.speed }} Km/h</li>
              <li>State : {{ weather.weather[0].main }}</li>
            </ul>
          </div>
        </div>
      </div>
    </main>
  </div>
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      userInput: "",
      apiKey: "5a0b81ce3710f1170f8982606b79d1f8",
      api: "https://api.openweathermap.org/data/2.5/",
      weather: {},
    };
  },
  methods: {
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
     fetch(`${this.api}/weather?q=${this.userInput}&appid=${this.apiKey}`).then((res)=>{
       return res.json().then((response)=>{
         this.weather = response;
       })
     })
    },
    dateBuild(){
        let d = new Date()
        let monthes =  ["Jan", "Feb", "March" , "April", "May", "Jun", "Jul", "Aug", "Sep", "October", "Nov" , "Dec"]
        let days =  ["Sun", "Mon", "Tue" , "Wen" , "Thu" , "Fri", "Sat"]
        let day = days[d.getDay()]
        let date = d.getDate()
        let year = d.getFullYear()
        let month = monthes[d.getMonth()]

        return `${day}   ${date}  ${month}  ${year}`
    }
  },
};
</script>

<style>
* {
  font-family: serif;
}
#app {
  background-size: cover;
  background-color: black;
  background-image: url("./assets/test.webp");
  background-position: bottom;
  opacity: 98%;
  overflow: hidden;
  padding: 20px;
}
main {
  min-height: 100vh;
  padding: 25px;
}
.search-box {
  width: 100%;
  margin-bottom: 30px;
}
.search-box .search-bar {
  display: block;
  width: 100%;
  padding: 15px;
  color: #313131;
  font-size: 20px;
  border: none;
  outline: none;
  background: none;
  background-color: rgb(32, 32, 32);
  color: #fff;
  overflow: hidden;
  border-top-right-radius: 10px;
  border-bottom-left-radius: 10px;
}
.container {
  display: Flex;
  justify-content: center;
}
.box {
  display: flex;
  flex-direction: column;
  align-items: center;
  padding: 20px;
  margin: 5px;
  border-top-right-radius: 10px;
  border-bottom-left-radius: 10px;
  width: 600px;
  height: 600px;
  color: white;
  font-size: 30px;
  font-weight: bolder;
}
.date {
  font-style: italic;
  font-size: 22px;
  padding-left: 15px;
}
.temp {
  display: flex;
  justify-content: center;
  background-color: #313131;
  padding: 10px;
  font-size: 55px;
  font-weight: bold;
  width: 200px;
  padding: 25px;
  border-radius: 10px;
  border: 2px solid black;
  opacity: 90%;
}
.weather {
  font-size: 30px;
  font-style: italic;
}
li {
  color: #fff;
  list-style: none;
}
.Error {
  color: #fff;
  text-align: center;
}
.btn {
  background-color: #313131;
  width: 250px;
  padding: 5px;
  text-align: center;
  color: #fff;
}
.btn:hover {
  background-color: #181616;
}
.btnCont{
  display : flex;
  justify-content: center;
}
</style>
