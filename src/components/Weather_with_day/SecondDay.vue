<template>
  <div class="secondDay">
    <div class="day_date">{{this.secondDay.info.date}}</div>
    <div class="min_max_temp">
      <div>Min.temp:{{this.secondDay.dayTempMin+"°"}}</div>
      <div>Max.temp:{{this.secondDay.dayTempMax+"°"}}</div>
    </div>
    <div class="secondDay_info">
      <div>00:00-{{this.secondDay.info["0"]+"°"}}</div>
      <div>03:00-{{this.secondDay.info["1"]+"°"}}</div>
      <div>06:00-{{this.secondDay.info["2"]+"°"}}</div>
      <div>09:00-{{this.secondDay.info["3"]+"°"}}</div>
      <div>12:00-{{this.secondDay.info["4"]+"°"}}</div>
      <div>15:00-{{this.secondDay.info["5"]+"°"}}</div>
      <div>18:00-{{this.secondDay.info["6"]+"°"}}</div>
      <div>21:00-{{this.secondDay.info["7"]+"°"}}</div>
    </div>
  </div>
</template>

<script>
export default {
  name: "SecondDay",
  props:{
    secondDay: {
      type: Object,
      required: true,
    }
  }
}
</script>

<style scoped>
.secondDay_info{
  display: none;
}
.secondDay{
  background: white;
  border-bottom: 3px solid #00ABB3;
  width: 100%;
  font-size: 20px;
  height: 22%;
}
.secondDay:hover {
  transition: all 1s;
  height: 150px;
}
.secondDay:hover .secondDay_info{
  transition: all 5s ease-in;
  display: flex;
  flex-direction: column;
  flex-wrap: wrap;
  width: 100%;
  height: 70%;
  padding-top: 10px;
}
.secondDay_info div{
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
  .secondDay_info div {
    border: 1px solid #00ABB3;
    width: 33%;
    flex-direction: row;
  }
}
</style>