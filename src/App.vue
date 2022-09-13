<template>
 <div id="app" :class="typeof this.weather.main != 'undefined' && this.weather.main.temp > 16 ? 'warm' : 'cold'">
     <main>
          <header>
               <!-- weather icon and tilie of the weather...etc go here -->
          </header>
          <div class="search-box">
               <input
                    type="text"
                    class="search-bar"
                    placeholder="Search..."
                    v-model="query"
                    @keypress = "fetchWeather"

               >


          </div>
          <div class="weather-wrap" v-if="typeof weather.main !== 'undefined'">
               <div class="location-box">
                    <div class="location">{{weather.name}}, {{weather.sys.country}}</div>
                    <div class="date">{{dateBuilder()}}</div>
               </div>

               <div class="weather-box">
                    <div id="temp" class="temp">{{Math.round(weather.main.temp)}}&deg;C</div>
                    <div class="weather">{{weather.weather[0].main}}</div>
               </div>
          </div>
     </main>
 </div>
</template>

<script>
export default {
  name: 'App',
  data () {
     return {
          api_key: 'f869a3e824eef906d9aa441b72e61a59',
          url_base: 'https://api.openweathermap.org/data/2.5/',
          query: '',
          weather: {}
     }
  },
  methods: {
     async fetchWeather(e) {
          if(e.key === 'Enter') {
               const res = await fetch(`${this.url_base}weather?q=${this.query}&units=metric&APPID=${this.api_key}`)
               const data = await res.json()
               this.weather = data
          }
     },

     dateBuilder(){
          let d = new Date();
          let months = ['January', 'February', 'March', 'April', 'May', 'June', 'July', 'August', 'September', 'October', 'November', 'December']
          let days = ['Sunday', 'Monday', 'Tuesday', 'Wednesday', 'Thursday', 'Friday', 'Saturday'];

          let day = days[d.getDay()];
          let date = d.getDate();
          let month = months[d.getMonth()]
          let year = d.getFullYear();

          return `${day} ${date} ${month} ${year}`;

     },
//IMPLEMENT THIS FUNCTION TE CHANGE BG IMAGE OF THE APP CONTAINER
//      backgroundChange(){
//           const temp = document.getElementById('temp');
//           temp.addEventListener('onchange', () => {
//                if (typeof this.weather.main != 'undefined' && this.weather.main.temp < 16)
//                document.getElementById('app').style.backgroundImage = "url('./assets/cold-bg.jpg')";
//                if(typeof this.weather.main != 'undefined' && this.weather.main.temp > 16)
//                document.getElementById('app').style.backgroundImage = "url('./assets/warm-bg.jpg')";
//           })
//
//      }
  }
}
</script>

<style>

     * {
          margin: 0;
          padding: 0;
          box-sizing: border-box;
     }
     body{
          font-family: 'mont serrat', sans-serif;
     }

     #app {
          background-image: linear-gradient(blue 0%, red 45%, orange 75%, yellow 100%);
          background-size: cover;
          background-position: bottom;
          transition: 0.7s ease;
     }

     #app.warm {
          background-image: url(./assets/warm-bg.jpg);
     }

      #app.cold {
          background-image: url(./assets/cold-bg.jpg);
     }

     main{
          min-height: 100vh;
          padding: 25px;
          background-image: linear-gradient(to bottom, rgba(0, 0, 0, 0.25), rgba(0, 0, 0, 0.75))
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
          border-radius: 16px 0px 16px 0px;
          transition: 0.8s;
     }

     .search-box .search-bar:focus {
          background-color: rgba(255, 255, 255, 0.75);
          box-shadow: 0px 0px 16px rgba(0, 0, 0, 0.25);
          border-radius: 0px 16px 0px 16px;

     }

     .location-box .location {
          color: #fff;
          font-size: 34px;
          font-weight: 500;
          text-align: center;
          text-shadow: 1px 3px rgba(0, 0, 0, 0.25);
     }

     .location-box .date {
          color: #fff;
          font-size: 18px;
          font-weight: 300;
          font-style:italic;
          text-align: center;
     }

     .weather-box {
          text-align: center;
     }

     .weather-box .temp {
          display: inline-block;
          padding: 10px 25px;
          color:#fff;
          font-size: 102px;
          font-weight: 900;
          text-shadow: 1px 3px rgba(0, 0, 0, 0.25);
          background-color: rgba(255, 255, 255, 0.25);
          border-radius: 16px;
          margin: 30px 0px;
          box-shadow: 3px 6px Rgba(0, 0, 0, 0.25);
     }

     .weather-box .weather{
          color:#fff;
          font-size: 48px;
          font-weight: 700;
          font-style:italic;
          text-shadow: 3px 6px rgba(0, 0, 0, 0.25);
     }



</style>
