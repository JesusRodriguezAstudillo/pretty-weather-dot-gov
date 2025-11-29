<script setup lang="ts">
import { ref } from 'vue'

const baseUrl = 'https://api.weather.gov'

const lon = ref(null)
const lat = ref(null)

async function weatherGovGet(url: string) {
  const response = await fetch(url, {
    method: 'GET',
    headers: {
      'User-Agent': 'prettyWeatherDotGov',
    },
  })

  // need error handling
  return await response.json()
}

async function getWeatherByLatLong() {
  const url = `${baseUrl}/points/${lat.value},${lon.value}`

  const responseData = await weatherGovGet(url)
  console.log(responseData)

  // get responseData["properties"]["forecastHourly"], pass it to a child component and render the data in a nice format

  // use a separate component to get the 7 day forcast

  return
}
</script>

<template>
  <form>
    <div>
      <span data-placeholder="Latitude">Latitude</span>
      <input type="number" v-model="lon" label="Enter Your Latittude" />
    </div>
    <div>
      <span>Longitude</span>
      <input type="number" v-model="lat" label="Enter Your Longitude" />
    </div>
    <button @click.prevent="getWeatherByLatLong">Get Hourly Weather</button>
  </form>
</template>
