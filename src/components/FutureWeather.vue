<template>
  <div class="futureWeather">
    <first-day :firstDay="this.first_day" class="future_day" ></first-day>
    <second-day :secondDay="this.second_day" class="future_day" ></second-day>
    <third-day :thirdDay="this.third_day" class="future_day" ></third-day>
    <fourty-day :fourty-day="this.fourty_day" class="future_day" ></fourty-day>
  </div>
</template>

<script>
import firstDay from "@/components/Weather_with_day/FirstDay";
import secondDay from "@/components/Weather_with_day/SecondDay";
import thirdDay from "@/components/Weather_with_day/ThirdDay";
import fourtyDay from "@/components/Weather_with_day/FourtyDay";

export default {
  components: {firstDay,secondDay,thirdDay,fourtyDay},
  props: {
    name: {
      type: String,
      required: true,
    }
  },
  data(){
    return {
      first_day: {
        info: {
          date: "",
          "0": "",
          "1": "",
          "2": "",
          "3": "",
          "4": "",
          "5": "",
          "6": "",
          "7": "",
        },
        dayTempMin:[],
        dayTempMax:[],
      },
      second_day:{
        info: {
          date: "",
          "0": "",
          "1": "",
          "2": "",
          "3": "",
          "4": "",
          "5": "",
          "6": "",
          "7": "",
        },
        dayTempMin:[],
        dayTempMax:[],
      },
      third_day:{
        info: {
          date: "",
          "0": "",
          "1": "",
          "2": "",
          "3": "",
          "4": "",
          "5": "",
          "6": "",
          "7": "",
        },
        dayTempMin:[],
        dayTempMax:[],
      },
      fourty_day:{
        info: {
          date: "",
          "0": "",
          "1": "",
          "2": "",
          "3": "",
          "4": "",
          "5": "",
          "6": "",
          "7": "",
        },
        dayTempMin:[],
        dayTempMax:[],
      },
      currentDayTime:{
        "0": "",
        "1": "",
        "2": "",
        "3": "",
        "4": "",
        "5": "",
        "6": "",
        "7": "",
      },
      currentTime: "",
    }
  },
  mounted() {
    this.getFutureWeather()
  },
  watch:{
    name: async function(){
      this.first_day.dayTempMin = [];
      this.first_day.dayTempMax = [];
      this.second_day.dayTempMin = [];
      this.second_day.dayTempMax = [];
      this.third_day.dayTempMin = [];
      this.third_day.dayTempMax = [];
      this.fourty_day.dayTempMin = [];
      this.fourty_day.dayTempMax = [];

      this.currentDayTime["0"] = "";
      this.currentDayTime["1"] = "";
      this.currentDayTime["2"] = "";
      this.currentDayTime["3"] = "";
      this.currentDayTime["4"] = "";
      this.currentDayTime["5"] = "";
      this.currentDayTime["6"] = "";
      this.currentDayTime["7"] = "";
      this.getFutureWeather()
    },
  },
  methods:{
    getFutureWeather: async function() {
      const city = this.name
      const key = "3954b4d2e94e091bf09bfecaad3ea648";

      const baseUrl_geocoder = `http://api.openweathermap.org/geo/1.0/direct?q=${city}&appid=${key}`
      const response = await fetch(baseUrl_geocoder);
      const geocoder_data = await response.json();
      const lat = geocoder_data[0].lat
      const lon = geocoder_data[0].lon



      const baseUrl = `http://api.openweathermap.org/data/2.5/forecast?lat=${lat}&lon=${lon}&appid=${key}&units=metric`
      const response_weather = await fetch(baseUrl);
      const futureWeather_data = await response_weather.json();
      const futureWeatherTime = Number(futureWeather_data.list[0].dt_txt.substring(10,13))
      let currentLiveTime = futureWeather_data.city.timezone / 3600
      let realTime = futureWeatherTime + currentLiveTime

      if (realTime > 24){
        realTime = realTime - 24}

      if(realTime < 3){
        this.currentTime = 7
      } else if (realTime < 6){
        this.currentTime = 6
      } else if (realTime  < 9){
        this.currentTime = 5
      }else if (realTime  < 12){
        this.currentTime = 4
      }else if (realTime  < 15){
        this.currentTime = 3
      }else if (realTime <  18){
        this.currentTime = 2
      }else if (realTime  < 21){
        this.currentTime = 1
      } else if (realTime  < 24){
        this.currentTime = 0
      }



      const firstDate = futureWeather_data.list[8].dt_txt
      const secondDate = futureWeather_data.list[16].dt_txt
      const thirdDate = futureWeather_data.list[24].dt_txt
      const fourtyDate = futureWeather_data.list[33].dt_txt


      const index_firstDay = this.currentTime;
      const index_secondDay = this.currentTime + 8;
      const index_thirdDay = this.currentTime + 16;
      const index_fourtyDay = this.currentTime + 24;



      let index_t = 7;
      for (let i = 1; i <= index_firstDay ; i++ ){
        this.currentDayTime[`${index_t}`] = Math.round(futureWeather_data.list[index_firstDay - i].main.temp_max)
        index_t--
      }



      for (let i = 0; i < 8; i++) {
        this.first_day.info[`${i}`] = Math.round(futureWeather_data.list[index_firstDay + i].main.temp_max)
        this.first_day.dayTempMin.push(this.first_day.info[`${i}`]);
        this.first_day.dayTempMax.push(this.first_day.info[`${i}`]);
        this.first_day.info.date = firstDate.substr(5, 5).split('-').reverse().join('-');
      }
      this.first_day.dayTempMax = Math.max.apply(null, this.first_day.dayTempMax)
      this.first_day.dayTempMin = Math.min.apply(null, this.first_day.dayTempMin)

      for (let i = 0; i < 8; i++) {
        this.second_day.info[`${i}`] = Math.round(futureWeather_data.list[index_secondDay + i].main.temp_max)
        this.second_day.dayTempMin.push(this.second_day.info[`${i}`]);
        this.second_day.dayTempMax.push(this.second_day.info[`${i}`]);
        this.second_day.info.date = secondDate.substr(5, 5).split('-').reverse().join('-');
      }
      this.second_day.dayTempMax = Math.max.apply(null, this.second_day.dayTempMax)
      this.second_day.dayTempMin = Math.min.apply(null, this.second_day.dayTempMin)

      for (let i = 0; i < 8; i++) {
        this.third_day.info[`${i}`] = Math.round(futureWeather_data.list[index_thirdDay + i].main.temp_max)
        this.third_day.dayTempMin.push(this.third_day.info[`${i}`]);
        this.third_day.dayTempMax.push(this.third_day.info[`${i}`]);
        this.third_day.info.date = thirdDate.substr(5, 5).split('-').reverse().join('-');
      }
      this.third_day.dayTempMax = Math.max.apply(null, this.third_day.dayTempMax)
      this.third_day.dayTempMin = Math.min.apply(null, this.third_day.dayTempMin)

      for (let i = 0; i < 8; i++) {
        this.fourty_day.info[`${i}`] = Math.round(futureWeather_data.list[index_fourtyDay + i].main.temp_max)
        this.fourty_day.dayTempMin.push(this.fourty_day.info[`${i}`]);
        this.fourty_day.dayTempMax.push(this.fourty_day.info[`${i}`]);
        this.fourty_day.info.date = fourtyDate.substr(5, 5).split('-').reverse().join('-');
      }
      this.fourty_day.dayTempMax = Math.max.apply(null, this.fourty_day.dayTempMax)
      this.fourty_day.dayTempMin = Math.min.apply(null, this.fourty_day.dayTempMin)

      this.$emit('time', this.currentDayTime)
    },
  },
}
</script>

<style scoped>
.futureWeather{
  background: white;
  border-radius: 10px;
  border: 3px solid #00ABB3;
  font-size: 15px;
  width: 100%;
}
.future_day{
  padding-bottom: 8px;
  width: 100%;
}

</style>