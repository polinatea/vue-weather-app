<template>
<main class="container text-white">
    <div class="mt-8 flex justify-center gap-8">
    <input type="text" class="bg-transparent border-b focus:outline-none " v-model="input" placeholder="Search places..." />
    <button @click="searchWeather" class="border-2 p-1 rounded-sm transition duration-150 ease-in-out hover:scale-110">Искать</button>
    </div>

    <div class="mt-8 flex justify-center">
    <div v-if="errored=='error'" key="somekeyhere">
      <p>Город не найден</p>
    </div>

    <div v-if="errored=='no error'" key="somekeyherxe" class="flex flex-col gap-4">
      <p>Температура воздуха: {{weather["temperature"]}} °C</p>
      <p>Скорость ветра: {{weather["windspeed"]}} м/с</p>
    </div>
    </div>
</main>
</template>

<script setup>
    import { ref } from "vue";
    import axios from 'axios'
    let input = ref("");
    let weather = ref(null);
    let errored =ref(null);
    const searchWeather = async () =>{
        if(input.value != " "){
            try{
            const result = await axios.get('https://geocode-maps.yandex.ru/1.x/?apikey=49e7b902-73b4-431d-8b04-330c8c80f907&geocode='+input.value+'&format=json')
            let coords = result["data"]["response"]["GeoObjectCollection"]["featureMember"][0]["GeoObject"]["Point"]["pos"]
            coords = coords.split(" ");       
            await axios.get('https://api.open-meteo.com/v1/forecast?latitude='+coords[1]+'&longitude='+coords[0]+'&current_weather=true')
            .then(data1 => weather.value=data1)
            console.log(weather.value)
            weather.value=weather.value["data"]["current_weather"]
            errored.value="no error"
        } catch{
            errored.value = "error"
        }
    }
    return;
}
</script>