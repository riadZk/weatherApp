<template>
  <!-- :class="typeof weather.main != 'undefined' && weather.main.temp > 16 ? 'warm' : '' -->
  <div id="app">
    <main>
      <div class="search-box mb-3">
        <form class="">
          <input
            type="text"
            class="search-bar"
            placeholder="Enter your city"
            v-model="ville"
          />
          <button @click.prevent="fetchWeather()" style="display: none">
            ville
          </button>
        </form>
      </div>
      <div class="weather-wrap" v-if="typeof weather.main != 'undefined'">
        <div class="row wrap">
          <div class="location">
            {{ weather.name }}, {{ weather.sys.country }}
          </div>
          <div class="date">{{ dateBuilder() }}</div>
          <div class="temp">{{ Math.round(weather.main.temp) }}°c</div>
          <img :src="weatherIcons[weather.weather[0].icon]" />
          <div class="temp-des">{{ weather.weather[0].description }}</div>
          <div class="wind-speed">Wind Spead : {{ weather.wind.speed }}</div>
        </div>
      </div>
    </main>
  </div>
</template>
<script>
import axios from "axios";
import icon01d from "@/assets/01d.svg";
import icon01n from "@/assets/01n.svg";
import icon02d from "@/assets/02d.svg";
import icon02n from "@/assets/02n.svg";
import icon03d from "@/assets/03d.svg";
import icon03n from "@/assets/03n.svg";
import icon04d from "@/assets/04d.svg";
import icon04n from "@/assets/04n.svg";
import icon09d from "@/assets/09d.svg";
import icon09n from "@/assets/09n.svg";
import icon10d from "@/assets/10d.svg";
import icon10n from "@/assets/10n.svg";
import icon11d from "@/assets/11d.svg";
import icon11n from "@/assets/11n.svg";
import icon13d from "@/assets/13d.svg";
import icon13n from "@/assets/13n.svg";
import icon50d from "@/assets/50d.svg";
import icon50n from "@/assets/50n.svg";

export default {
  name: "app",
  data() {
    return {
      apiKey: process.env.VUE_APP_API_KEY,
      url: process.env.VUE_APP_BASE_URL,
      ville: "",
      weather: {},
      weatherIcons: {
        "01d": icon01d,
        "01n": icon01n,
        "02n": icon02n,
        "02d": icon02d,
        "03d": icon03d,
        "03n": icon03n,
        "04d": icon04d,
        "04n": icon04n,
        "09d": icon09d,
        "09n": icon09n,
        "10d": icon10d,
        "10n": icon10n,
        "11d": icon11d,
        "11n": icon11n,
        "13d": icon13d,
        "13n": icon13n,
        "50d": icon50d,
        "50n": icon50n,
      },
    };
  },
  methods: {
    fetchWeather() {
      axios
        .get(
          `${this.url}weather?q=${this.ville}&units=metric&APPID=${this.apiKey}`
        )
        .then((res) => (this.weather = res.data))
        .catch((err) => console.log(err));
    },
    dateBuilder() {
      let d = new Date();
      let months = [
        "January",
        "February",
        "March",
        "April",
        "May",
        "June",
        "July",
        "August",
        "September",
        "October",
        "November",
        "December",
      ];
      let days = [
        "Sunday",
        "Monday",
        "Tuesday",
        "Wednesday",
        "Thursday",
        "Friday",
        "Saturday",
      ];
      let day = days[d.getDay()];
      let date = d.getDate();
      let month = months[d.getMonth()];
      let year = d.getFullYear();
      return `${day} ${date} ${month} ${year}`;
    },
  },
};
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  font-family: "Poppins", sans-serif;
}
#app {
  background-image: url("./assets/clouds-sun-rays-sky.jpg");
  background-size: cover;
  background-position: center;
  height: 100vh;
  background-attachment: fixed;
  transition: 0.4s;
}
main {
  min-height: 100vh;
  padding: 25px;
  background-image: linear-gradient(
    to bottom,
    rgba(0, 0, 0, 0.55),
    rgba(0, 0, 0, 0.75)
  );
  display: flex;
  justify-content: top;
  align-items: center;
  flex-direction: column;
  padding-top: 80px;
  color: aliceblue;
  text-align: center;
}
input {
  width: 450px;
  height: 40px;
  padding: 10px;
  border: none;
  border-radius: 0 20px;
  outline: none;
  background: none;
  background-color: rgba(255, 255, 255, 0.5);
  color: white;
  font-size: 16px;
}
input::placeholder {
  color: rgb(255, 255, 255);
}
img {
  height: 150px;
  width: 200px;
}
.weather-wrap {
  width: auto;
  height: auto;
  border-radius: 50px;
  background: rgba(119, 158, 177, 0.29);
  margin: 20px 0;
}
.wrap {
  display: flex;
  flex-direction: column;
  align-items: center;
  padding: 20px;
}
.location {
  font-weight: bold;
  font-size: 30px;
}
.date {
  font-size: 14px;
  color: rgb(192, 192, 192);
}
.temp-main {
  display: flex;
  align-items: center;
  align-items: center;
  align-self: center;
  margin: 10px;
}
.temp {
  font-size: 50px;
  font-weight: bold;
}
.temp-des {
  font-size: 20px;
  font-weight: bold;
  margin-bottom: 30px;
  text-align: center;
}
.wind-speed {
  font-size: 15px;
  font-weight: bold;
}
</style>
