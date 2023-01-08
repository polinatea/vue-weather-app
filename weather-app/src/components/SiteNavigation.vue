<template>

  <header class="sticky top-0 bg-weather-primary shadow-lg py-6 flex justify-center">
    <p class="text-2xl text-white ">Узнай погоду, где хочешь</p>
  </header>
</template>

<script setup>

</script>



<!-- <script setup>
import { onMounted, ref } from "vue";
import axios from 'axios'
let input = ref("");
let result = ref(null);
let weather = ref(" ");
let errored =false;
const searchWeather = async () =>{

  await axios.get('https://geocode-maps.yandex.ru/1.x/?apikey=49e7b902-73b4-431d-8b04-330c8c80f907&geocode='+input.value+'&format=json')
  .then(data=> result.value = data)

  if(result.value["data"]["response"]["GeoObjectCollection"]["featureMember"][0]==undefined){
    errored=true;
    console.log("eke")
  }
  
  else{
  let coords = result.value["data"]["response"]["GeoObjectCollection"]["featureMember"][0]["GeoObject"]["Point"]["pos"]
  coords = coords.split(" ");
  console.log("coordinates:    "+coords)
  errored=false;
  
  
  await axios.get('https://api.open-meteo.com/v1/forecast?latitude='+coords[1]+'&longitude='+coords[0]+'&current_weather=true')
  .then(data1 => weather.value=data1)

  weather.value=weather.value["data"]["current_weather"]
  }
  return(weather.value)

}

</script>

<template>
  <header>
    
<h1>Погода</h1>

  </header>

  <main>
    <input type="text" v-model="input" placeholder="Search places..." />
    <button @click="searchWeather">Искать</button>

    <div v-if="errored" key="somekeyhere">
      <p>Город не найден</p>
    </div>

    <div v-if="errored==false" key="somekeyherxe">
      <p>{{weather["temperature"]}}</p>
      <p>{{weather["windspeed"]}}</p>
    </div>
  </main>
</template>

<style scoped>


</style> -->