<template>
  <div class="fourtyDay">
    <div class="day_date">{{this.fourtyDay.info.date}}</div>
    <div class="min_max_temp">
      <div>Min.temp:{{this.fourtyDay.dayTempMin+"°"}}</div>
      <div>Max.temp:{{this.fourtyDay.dayTempMax+"°"}}</div>
    </div>
    <div class="fourtyDay_info">
      <div>00:00-{{this.fourtyDay.info["0"]+"°"}}</div>
      <div>03:00-{{this.fourtyDay.info["1"]+"°"}}</div>
      <div>06:00-{{this.fourtyDay.info["2"]+"°"}}</div>
      <div>09:00-{{this.fourtyDay.info["3"]+"°"}}</div>
      <div>12:00-{{this.fourtyDay.info["4"]+"°"}}</div>
      <div>15:00-{{this.fourtyDay.info["5"]+"°"}}</div>
      <div>18:00-{{this.fourtyDay.info["6"]+"°"}}</div>
      <div>21:00-{{this.fourtyDay.info["7"]+"°"}}</div>
    </div>
  </div>
</template>

<script>
export default {
  name: "FourtyDay",
  props:{
    fourtyDay: {
      type: Object,
      required: true,
    }
  }
}
</script>

<style scoped>
.fourtyDay_info{
  display: none;
}
.fourtyDay{
  background: white;
  border-bottom: 3px solid #00ABB3;
  width: 100%;
  font-size: 20px;
  height: 22%;
}
.fourtyDay:hover {
  transition: all 1s;
  height: 150px;
}
.fourtyDay:hover .fourtyDay_info{
  transition: all 5s ease-in;
  display: flex;
  flex-direction: column;
  flex-wrap: wrap;
  width: 100%;
  height: 70%;
  padding-top: 10px;
}
.fourtyDay_info div{
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
  .fourtyDay_info div {
    border: 1px solid #00ABB3;
    width: 33%;
    flex-direction: row;
  }
}
</style>