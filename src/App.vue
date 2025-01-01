<template>
  <div 
    class="app" 
    :style="{ 
      'background': 'linear-gradient(to bottom right, #8a2be2, #ee82ee)' 
    }"
  >
   <loader v-if="loading" />
    <error-popup class="wrapper" v-if="displayError" :message="errorMsg" />
    
    <search-bar
      :dataList="searchHistory"
      @onSearch="getCityWeather"
      placeholder="Enter city name"
      buttonValue="Search" />

    <weather-widget
      :city="weatherWidgetData?.name"
      :icon="weatherWidgetData?.weatherIcon"
      :temp="weatherWidgetData?.temp"
      :tempMax="weatherWidgetData?.tempMax"
      :tempMin="weatherWidgetData?.tempMin"
      :feelsLike="weatherWidgetData?.feelsLike"
      :weatherDescription="weatherWidgetData?.weatherDescription" />
      
    <div class="wrapper">
      <info-box
        v-for="(detail, i, index) in weatherDetails"
        :style="index === 0 && 'border-top-left-radius: 15px; border-top-right-radius: 15px'"
        :key="i"
        :title="detail?.title"
        :val="detail?.val"
        :iconSrc="detail?.icon" />
    </div>
  </div>
</template>

<script>
import { mapState } from 'vuex'
import SearchBar from './components/SearchBar'
import WeatherWidget from './components/WeatherWidget'
import InfoBox from './components/InfoBox'
import Loader from './components/Loader'
import ErrorPopup from './components/ErrorPopup'

export default {
  name: 'App',
  components: {
    SearchBar,
    WeatherWidget,
    InfoBox,
    Loader,
    ErrorPopup
  },
  computed: {
    ...mapState(['loading', 'weatherDetails', 'weatherWidgetData', 'currentHour', 'displayError', 'searchHistory', 'errorMsg']),
    getCurrentTimezone() {
      let sunriseHour = Number(this.weatherDetails?.sunrise?.val.substr(0, this.weatherDetails.sunrise.val.indexOf(':')))
      let sunsetHour = Number(this.weatherDetails?.sunset?.val.substr(0, this.weatherDetails.sunset.val.indexOf(':')))

      switch (true) {
        case this.currentHour === sunsetHour:
          return 'sunset'
        case this.currentHour === sunriseHour:
          return 'sunrise'
        case this.currentHour > sunsetHour || this.currentHour < sunriseHour:
          return 'night'
        default:
          return 'day'
      }
    },
    getCurrentWeatherDescription() {
      let weatherDescription = this.weatherWidgetData?.weatherDescription

      switch (weatherDescription) {
        case 'Clouds':
          return 'cloudy'
        case 'Clear':
          return 'sunny'
        case 'Rain' || 'Drizzle' || 'Thunderstorm':
          return 'rainy'
        case 'Snow':
          return 'snowy'
        default:
          return 'mist'
      }
    }
  },
  methods: {
    getCityWeather(city) {
      this.$store.dispatch('getCityWeather', city)
    }
  },
  created() {
    this.getCityWeather()
  }
}
</script>

<style>
@font-face {
  font-family: Luxia-Regular;
  src: url('./font/Luxia-Regular.otf');
}

:root {
  font-size: 18px;
}
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
.app {
  width: 100vw;
  height: 100vh;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  align-items: center;
  background-position: center;
  background-size: cover;
  background-repeat: no-repeat;
}
#app {
  font-family: Luxia-Regular, Avenir, Helvetica, Arial, sans-serif;
  text-align: center;
  color: #dbdbdb;
}
.wrapper {
  width: 100%;
  max-width: 800px;
}
.flex {
  display: flex;
  justify-content: center;
  align-items: center
}
.icon {
  width: 45px;
  height: 45px;
}
input {
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0);
  color: #a6a6a6;
  border: none;
  padding: 15px 30px;
  border-right: 1px solid #737373;
  font-size: 1rem;
  outline: none;
}
button {
  outline: none;
  padding: 15px 30px;
  border: none;
  background-color: rgba(0, 0, 0, 0);
  color: #a6a6a6;
  font-size: 1rem;
}
.container {
  background-color: rgba(0, 0, 0, 0.3);
  width: 100%;
}
</style>
