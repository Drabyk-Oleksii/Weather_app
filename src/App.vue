<template>
  <div class="app">
    <div class="weather_app" v-bind:class="{active: this.cityName}">
      <search @create="getCityName" class="search"></search>
      <current-weather :time="currentTimeWeather" v-if="cityName" :name="cityName" class="current_weather_block"></current-weather>
      <future-weather @time = "getCurrentTime" v-if="cityName" :name="cityName" class="future_weather_block"></future-weather>
      <div v-else class="background_weather"></div>
    </div>
  </div>
</template>

<script>
import search from "@/components/Search";
import currentWeather from "@/components/CurrentWeather";
import futureWeather from "@/components/FutureWeather";
export default {
  components: {
    search,currentWeather,futureWeather
  },
  data(){
    return {
      cityName: '',
      currentTimeWeather: '',
    }
  },
  methods: {
    getCityName(name){
      this.cityName = name;
    },
    getCurrentTime(time){
      this.currentTimeWeather = time;
    }
  },
}
</script>
<style scoped>
.app{
  height: 100vh;
  width: 100%;
  background: url("assets/main_background.jpg")0 0/cover no-repeat;
  padding-top: 100px;
  margin: 0;
}
.weather_app{
  margin: 200px auto 0;
  width: 90%;
  height: 20%;
  background: grey;
  border-radius: 15px;
  display: flex;
  flex-direction: column;
  align-items: center;
  opacity: 0.97;
}
.weather_app.active{
  height: 90%;
  margin: 0 auto;
}

.future_weather_block{
  width: 90%;
  height: 32%;
}
.current_weather_block {
  width: 90%;
  height: 45%;
}


</style>
