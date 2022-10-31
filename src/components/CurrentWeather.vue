<template>
  <div class="current_weather">
    <div class="weather_image">
      <img v-bind:src="this.weather.current_weather_icon"  alt="Loading..">
    </div>
    <div class="current_weather_info">
      <div>Current temp:{{weather.current_temp}}°</div>
      <div>Feels like:{{weather.feels_like}}</div>
      <div>Temp min:{{weather.temp_min}}°</div>
      <div>Temp max:{{weather.temp_max}}°</div>
      <div>Humidity:{{weather.humidity}}</div>
      <div class="weather_description">{{weather.description}}</div>
    </div>
    <div class="current_weather_time">
      <div v-if="this.time['0']">00:00 -  {{this.time[`${0}`]}}°</div>
      <div v-if="this.time['1']">03:00 -  {{this.time[`${1}`]}}°</div>
      <div v-if="this.time['2']">06:00 -  {{this.time[`${2}`]}}°</div>
      <div v-if="this.time['3']">09:00 -  {{this.time[`${3}`]}}°</div>
      <div v-if="this.time['4']">12:00 -  {{this.time[`${4}`]}}°</div>
      <div v-if="this.time['5']">15:00 -  {{this.time[`${5}`]}}°</div>
      <div v-if="this.time['6']">18:00 -  {{this.time[`${6}`]}}°</div>
      <div v-if="this.time['7']">21:00 -  {{this.time[`${7}`]}}°</div>
    </div>
  </div>
</template>

<script>

export default {
  props: {
    name: {
      type: String,
      required: true,
    },
    time: {
      type: Object,
      required: true,
    }
  },
  data() {
    return {
      weather: {
        current_temp: "",
        feels_like: "",
        temp_min: "",
        temp_max: "",
        humidity: "",
        current_weather_icon: "",
        description: "",
      },
    }
  },
  mounted() {
    this.getCurrentWeather()
  },
  watch: {
    name: function (){
      this.getCurrentWeather()
    }
  },
  methods: {
    getCurrentWeather: async function () {
      const city = this.name
      const key = "3954b4d2e94e091bf09bfecaad3ea648";
      const baseUrl_currentWeather = `https://api.openweathermap.org/data/2.5/weather?q=${city}&appid=${key}&units=metric`
      const response = await fetch(baseUrl_currentWeather);
      const currentWeatherdata = await response.json();
      const icon = currentWeatherdata.weather[0].icon
      this.weather.current_weather_icon = `http://openweathermap.org/img/wn/${icon}@2x.png`


      this.weather.current_temp = Math.round(currentWeatherdata.main.temp);
      this.weather.feels_like = Math.round(currentWeatherdata.main.feels_like);
      this.weather.temp_min = Math.round(currentWeatherdata.main.temp_min);
      this.weather.temp_max = Math.round(currentWeatherdata.main.temp_max);
      this.weather.humidity = Math.round(currentWeatherdata.main.humidity) + "%";
      this.weather.description = (currentWeatherdata.weather[0].description).toUpperCase()
    }
  }
}
</script>

<style scoped>
.current_weather{
  background: white;
  border-radius: 10px;
  display: flex;
  flex-direction: column;
  align-items: center;
}
.weather_image{
  background: grey;
  width: 40%;
  display: flex;
  justify-content: center;
  border-radius: 10px;
  height: 40%;
  margin-top: 5px;
  margin-bottom: 15px;
}
.current_weather_info{
  font-weight: bold;
  display: flex;
  flex-direction: column;
  align-items: center;
  margin-bottom: 10px;
}
.current_weather_time{
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  margin-bottom: 10px;
}
.current_weather_time div{
  border: 1px solid #00ABB3;
  padding: 5px;
  border-radius: 3px;
}
@media screen and (min-width:1000px) {
  .weather_image{
    width: 50%;
    max-width: 450px;
    height: 60%;
  }
  .current_weather{
    font-size: 20px;
  }
}
</style>