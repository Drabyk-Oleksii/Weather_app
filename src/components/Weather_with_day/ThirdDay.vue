<template>
  <div class="thirdDay">
    <div class="day_date">{{this.thirdDay.info.date}}</div>
    <div class="min_max_temp">
      <div>Min.temp:{{this.thirdDay.dayTempMin+"°"}}</div>
      <div>Max.temp:{{this.thirdDay.dayTempMax+"°"}}</div>
    </div>
    <div class="thirdDay_info">
      <div>00:00-{{this.thirdDay.info["0"]+"°"}}</div>
      <div>03:00-{{this.thirdDay.info["1"]+"°"}}</div>
      <div>06:00-{{this.thirdDay.info["2"]+"°"}}</div>
      <div>09:00-{{this.thirdDay.info["3"]+"°"}}</div>
      <div>12:00-{{this.thirdDay.info["4"]+"°"}}</div>
      <div>15:00-{{this.thirdDay.info["5"]+"°"}}</div>
      <div>18:00-{{this.thirdDay.info["6"]+"°"}}</div>
      <div>21:00-{{this.thirdDay.info["7"]+"°"}}</div>
    </div>
  </div>
</template>

<script>
export default {
  name: "ThirdDay",
  props:{
    thirdDay: {
      type: Object,
      required: true,
    }
  }
}
</script>

<style scoped>
.thirdDay_info{
  display: none;
}
.thirdDay{
  background: white;
  border-bottom: 3px solid #00ABB3;
  width: 100%;
  font-size: 20px;
  height: 22%;
}
.thirdDay:hover {
  transition: all 1s;
  height: 150px;
}
.thirdDay:hover .thirdDay_info{
  transition: all 5s ease-in;
  display: flex;
  flex-direction: column;
  flex-wrap: wrap;
  width: 100%;
  height: 70%;
  padding-top: 10px;
}
.thirdDay_info div{
  display: flex;
  justify-content: center;
  height: 24%;
  width: 50%;
}
.min_max_temp{
  display: flex;
  justify-content: space-around;
}
.day_date{
  text-align: center;
}
@media screen and (min-width:1000px) {
  .thirdDay_info div {
    border: 1px solid #00ABB3;
    width: 33%;
    flex-direction: row;
  }
}
</style>