<template>
  <div class="container">
    <h1 style="font-size: 3rem;">{{ city }}</h1>
    <div class="flex">
      <img 
        v-if="icon" 
        style="width: 150px; height: 150px;" 
        :src="`https://openweathermap.org/img/wn/${icon}@2x.png`" 
        alt="Weadher icon"> 
      <span style="font-size: 2.5rem">
        {{temp}}°C
      </span>
    </div>
    {{ tempMax }}°/{{ tempMin }}° <br>
    Feels like {{ feelsLike }}° <br>
    {{ weatherDescription }} <br>
  </div>
</template>

<script>
export default {
  name: 'WeatherWidget',
  props: {
    city: String,
    icon: String,
    temp: String || Number,
    tempMax: String || Number,
    tempMin: String || Number,
    feelsLike: String || Number,
    weatherDescription: String
  }
}
</script>

<style scoped>
.container {
  width: fit-content;
  padding: 30px 50px;
  border-radius: 15px;
}
</style>
