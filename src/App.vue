<template>
  <div id="app">
    <div class="container">
      <h1>Weather Radar</h1>
      <ZipCode v-on:updateWeather=updateWeather($event) v-on:updateTemp=updateTemp($event)></ZipCode>
      <Weather v-bind:temp="finTemp" v-bind:city="weatherInfo.name" v-bind:condition="condition" v-bind:conditionImg="imageUrl" v-bind:type="type"/>
      </div>
  </div>
</template>

<script>

import ZipCode from './components/ZipCode.vue'
import Weather from './components/Weather.vue'
import axios from 'axios';

export default {
  name: 'App',
  components: {
    ZipCode,
    Weather
  },
  data()
  {
    return{
      weatherInfo:"",
      zipInput:"",
      iniTemp:0,
      icon:"02d",
      imageUrl: "",
      type:"",
      finTemp:0,
      condition:""
    }
  },
  mounted()
  {
  
  },
  methods:
  {
    updateWeather(zip)
    {
      axios.get("https://api.openweathermap.org/data/2.5/weather?zip="+zip+",us&appid=960407da8a9c327e446e6e1ad12629df").then( (response) => {
        this.iniTemp = response.data.main.temp;
        this.weatherInfo = response.data;
        this.icon = this.weatherInfo.weather[0].icon;
        this.condition = this.weatherInfo.weather[0].description;
        this.imageUrl = "http://openweathermap.org/img/wn/"+this.icon+"@4x.png"
        

        if(document.getElementById('flexRadioDefault1').checked)
        {
          this.updateTemp(true);
        }
        else if(document.getElementById('flexRadioDefault2').checked)
        {
          this.updateTemp(false);
        }

      }, () => {
        alert("Please Enter US Zip Code");
      })
    },
    updateTemp(temperature)
    {
      if(temperature)
      {
        this.type = "°F";
        this.finTemp = ((this.iniTemp-273.15)*(9/5)+32).toFixed(2);
      }
      else if (temperature == false)
      {
        this.type = "°C";
        this.finTemp = (this.iniTemp - 273.15).toFixed(2);
      }
    }
    

  }
}
</script>

<style>

body{
  padding-top:60px;
  background-image: url(assets/weather.jpg);
  background-size: cover;
}
.container{
  background-color: rgb(4, 41, 97);
  padding:20px;
  color: aliceblue;
}
h1{
  text-align: center;
}
</style>
