<template>
  <div class="firstDay">
    <div class="day_date">{{this.firstDay.info.date}}</div>
    <div class="min_max_temp">
      <div>Min.temp:{{firstDay.dayTempMin+"°"}}</div>
      <div>Max.temp:{{firstDay.dayTempMax+"°"}}</div>
    </div>
    <div class="firstDay_info">
      <div>00:00-{{this.firstDay.info["0"]+"°"}}</div>
      <div>03:00-{{this.firstDay.info["1"]+"°"}}</div>
      <div>06:00-{{this.firstDay.info["2"]+"°"}}</div>
      <div>09:00-{{this.firstDay.info["3"]+"°"}}</div>
      <div>12:00-{{this.firstDay.info["4"]+"°"}}</div>
      <div>15:00-{{this.firstDay.info["5"]+"°"}}</div>
      <div>18:00-{{this.firstDay.info["6"]+"°"}}</div>
      <div>21:00-{{this.firstDay.info["7"]+"°"}}</div>
    </div>
  </div>
</template>

<script>
export default {
  name: "FirstDay",
  props:{
    firstDay: {
      type: Object,
      required: true,
    }
  },
  methods: {

  }
}

</script>

<style scoped>
.firstDay_info{
  display: none;
}
.firstDay{
  background: white;
  width: 97%;
  font-size: 20px;
  height: 22%;
  border-bottom: 3px solid #00ABB3;
}
.firstDay:hover {
  transition: all 1s;
  height: 150px;
}
.firstDay:hover .firstDay_info{
  transition: all 5s ease-in;
  display: flex;
  flex-direction: column;
  flex-wrap: wrap;
  width: 100%;
  height: 70%;
  padding-top: 10px;
}
.firstDay_info div{
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
  .firstDay_info div {
    border: 1px solid #00ABB3;
    width: 33%;
    flex-direction: row;
  }
}
</style>