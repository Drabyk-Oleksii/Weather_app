<template>
  <div class="search">
    <form v-on:submit.prevent="getCityName">
      <input class="input" type="text"  v-model="cityName" >
      <button @click="getCityName">SEARCH</button>
    </form>
  </div>
</template>

<script>
export default {
  name: "Search",
  data(){
    return {
      cityName: '',
    }
  },
  methods: {
    getCityName(){
      this.$emit('create', this.cityName)
    }

  }
}
</script>

<style scoped>
.search{
  margin-top:50px;
  width: 100%;
  display: flex;
  justify-content: center;
  height: 3vh;
  margin-bottom: 20px;
}
.search input{
  width: 85%;
  border-radius: 5px;
  border: 1px solid white;
  font-size: 3vh;
}
form{
  width: 70%;
  display: flex;
  justify-content: center;
  background: white;
  border-radius: 15px;
  height: 4vh;
}
button{
  background: #00ABB3;
  border: 1px solid #00ABB3;
  border-radius: 5px;
  color: black;
  width: 30%;
  font-size: 13px;
  font-weight: bold;
}
@media screen and (min-width:1000px){
  button{
    font-size: 20px;
  }
}
</style>