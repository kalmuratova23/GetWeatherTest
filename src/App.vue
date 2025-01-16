<script>
import axios from "axios"

export default{
  data(){
    return {
      city: "",
      error:"",
      info:null

    }
  },
  computed:{
    cityName(){
      return "«" + this.city + "»"
    },
    showTemp(){
      return "Temperature: " + this.info.main.temp
    },
    showFeelsLike(){
      return "Feels like: " + this.info.main.feels_like
    },
    showMinTemp(){
      return "Minimun temp: " + this.info.main.min_temp
    },
    showMaxTemp(){
      return "Maximum temp: " + this.info.main.max_temp
    }
  },
  methods:{
    getWeather(){
      if(this.city.trim().length<2) {
        this.error = "Enter city name greater than 2 characters:"
        return false
      }
      this.error = ""

      axios.get(`https://api.openweathermap.org/data/2.5/weather?q=${this.city}&units=metric&appid=a57ce06cfe9ccd4cb3dad21c9001c5db`)
          .then(res =>(this.info = res.data))
    }
  }
}
</script>

<template>
  <div class="wrapper">
    <h1>Weather App{{ }}</h1>
    <p>Know weather in your {{ city == "" ? "in your city" :cityName }} </p>
    <input type="text" v-model="city" placeholder="Enter your city">
    <button v-if="city != ''" @click="getWeather()">Get Weather</button>
    <button disabled v-else>Enter city name</button>
    <p class="error">{{ error }}</p>

    <div v-if="info!= null">
      <p>{{ showTemp}}</p>
      <p>{{ showFeelsLike}}</p>
      <p>{{ showMinTemp}}</p>
      <p>{{ showMaxTemp}}</p>
    </div>


  </div>
</template>

<style scoped>
.error{
  color: #d03939;
}

.wrapper{
  width: 900px;
  height: 500px;
  border-radius: 50px;
  padding: 20px;
  background: #1f0f24;
  text-align: center;
  color: #fff;
}
.wrapper h1{
  margin-top: 50px;
}
.wrapper p{
  margin-top: 20px;
}
.wrapper input{
  margin-top: 30px;
  background: transparent;
  border: 0;
  border-bottom: 2px solid #110813;
  color: #fcfcfc;
  font-size: 14px;
  padding: 5px 8px;
  outline: none;
}
.wrapper input:focus{
  border-bottom-color: #6e2d7d;
}
.wrapper button{
  background: #e3bc4d;
  color: #fff;
  border-radius: 10px;
  border: 2px solid #b99935;
  padding: 10px 15px;
  margin-left: 20px;
  cursor: pointer;
  transition: transform 500ms ease;
}
.wrapper button:hover{
  transform: scale(1.1) translateY(-5px);
}
.wrapper button:disabled{
  background: #746027;
  cursor: not-allowed;
}
</style>
