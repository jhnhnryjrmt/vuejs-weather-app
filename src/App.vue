<template>
  <div id="app" :class="typeof weather.main != 'undefined' && weather.main.temp > 16 ? 'warm' : '' ">
    <main>
      <div class="search-box">
        <input 
          type="text" 
          class="search-bar" 
          v-model="query" 
          placeholder="Search..."
          @keypress="fetchWeather" 
        />
      </div>

      <div class="weather-wrap">
        <div class="location-box">
          <div class="location">San Antonio, USA</div>
          <div class="date">Friday 30 September 2021</div>
        </div>

        <div class="weather-box">
          <div class="temp">23°c</div>
          <div class="weather">Windy</div>
        </div>
      </div>

    </main>
  </div>
</template>

<script>

export default {
  name: 'app',
  data() {
    return {
      api_key: 'a6e572eb1f12837480051b0a9f354dad',
      url_base: 'api.openweathermap.org/data/2.5/',
      query: '',
      weather: {}
    }
  },
  methods: {
    fetchWeather(e) {
      if(e.key == "Enter") {
        fetch(`${this.url_base}weather?q=${this.query}&units=metric&APPID=${this.api_key}`)
          .then(res => {
            return res.json();
          }).then(this.setResults);
      }
    },
    setResults (results) {
      this.weather = results;
    }
  }
}
</script>

<style>
  * {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
  }

  body {
    font-family: 'montserrat', sans-serif;
  }

  #app {
    background-image: url('./assets/cold-bg.jpg');
    background-size: cover;
    background-position: bottom;
    transition: 0.4s;
  }

  #app.warm {
    background-image: url('./assets/warm-bg.jpg');
  }

  main {
    min-height: 100vh;
    padding: 25px;
    background-image: linear-gradient(to bottom, rgba(0, 0, 0, 0.25), rgba(0, 0, 0, 0.75));
  }

  .search-box {
    width: 100%;
    margin-bottom: 30px;
  }

  .search-box .search-bar {
    display: block;
    width: 100%;
    padding: 15px;
    color: #313131;
    font-size: 20px;
    appearance: none;
    border: none;
    outline: none;
    background: none;
    box-shadow: 0px 0px 8px rgba(0, 0, 0, 0.25);
    background-color: rgba(255, 255, 255, 0.5);
    border-radius: 0px 16px 0px 16px;
    transition: 0.4s;
  }
</style>
