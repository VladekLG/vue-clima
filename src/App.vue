<template>
  <v-app id="app">
    <main>
      <template>
        <!-- Buscador -->
        <v-card class="search-box" color="#263238">
          <input
            type="text"
            class="search-bar"
            placeholder="Escribe una ciudad..."
            v-model="query"
            @keypress="fetchWeather"
          />
        </v-card>


        <!-- Clima datos/weather wrap -->
        <div class="mx-auto mt-10 weather-wrap" max-width="368" id="card1" v-if="typeof weather.main != 'undefined'">
          
          <div class='location-box'>
            <!-- location -->
            <div class="text-h5 text-center location">{{weather.name}}, {{weather.sys.country}}</div>
            <!-- date -->
          </div>

          <!-- clima-box -->

          <div class="mt-2 weather-box">
            <!-- temp -->
            <v-col class="text-h2 text-center temp"> {{Math.round(weather.main.temp)}}°C</v-col>
            <!-- clima -->
            <v-col class="text-h4 text-center weather">{{weather.weather[0].main}}</v-col>
          </div>
        </div>
      </template>
    </main>
  </v-app>
</template>

<script>




export default {
  name: "app",

  data: () => ({
    api_key: "ae622854af7f931b649254c51d1bd52c",
    url_base: "https://api.openweathermap.org/data/2.5/",
    query: "",
    weather: {},
  }),

  methods: {
    fetchWeather(e){
      if (e.key == "Enter"){
        fetch(`${this.url_base}weather?q=${this.query}&units=metric&APPID=${this.api_key}`)
          .then(res =>{
            return res.json();
          }).then(this.verResultados);

      }

    },
    verResultados (resultados){

    this.weather = resultados;
    }
  },
};
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

#app {
  background-image: url(./assets/img/clima.jpg);
  background-size: cover;
  background-position: bottom;
  transition: 0.4s;
}
#card1 {
  background-image: url(./assets/img/rain.jpg);
  background-size:contain;
  background-position: bottom;
  transition: 0.4s;
  height: 25vh;
  
}
main {
  min-height: 100vh;
  padding:25px;
  background-image: linear-gradient(
    to bottom,
    rgba(0, 0, 0, 0.25),
    rgba(0, 0, 0, 0.75)
  );
}

/* search box */

.search-box {
  width: 100%;
  margin-bottom: 30px;
  color: white;
  border-radius: 100px;
}
.search-box .search-bar {
  display: block;
  width: 100%;
  padding: 15px;

  color: #f1f1f1;
  font-size: 20px;
  text-shadow: 1px 3px rgba(0, 0, 0, 0.25);

  appearance: none;
  border: none;
  outline: none;
  background: none;

  background-color: rgba(255, 255, 255 0.15);
}

/* location-box styles */

.location-box .location {
  color: white;
  font-weight: 500;
  text-shadow: 1px 3px rgba(0, 0, 0, 0.25);
}

.location-box .date {
  color: white;
  font-weight: 300;
  font-style: oblique;
}

/* weahter box styles */



.weather-box .temp {
  color: white;
  font-weight: bolder;
  text-shadow: 5px 3px rgba(0, 0, 0, 0.25);
  
}

.weather-box .weather {
  color: white;
  font-weight: 350;
  text-shadow: 1px 3px rgba(0, 0, 0, 0.25);
}
</style>
