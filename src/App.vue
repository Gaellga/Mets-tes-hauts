<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/img/icon.png">
    <h1>Welcome to the weathsite</h1>
    <form @submit.prevent="getWeather()">
      <div class="row">
        <div class="offset-md-3 col-md-6">
          <div class="form-group">
            <input v-model="inputdata" type="text" class="form-control" aria-describedby="browsecity" placeholder="Enter city">
          </div>
        </div>
      </div>
      <div class="row">
        <div class="offset-md-2 col-md-8 border border-green">
          <div class="row">
            <div class="col-md-12 border border-green">
              <div class="row">
                <div class="col-md-3">{{icon}}</div>
                <div class="col-md-5"><p>{{name}}</p><p>{{currentTemp}}</p></div>
                <div class="col-md-4"><p>Précipitations : {{pressure}}</p>Humidité : {{humidity}}<p></p>Vent : {{wind}}<p></p></div>
              </div>
            </div>
          </div>
          <div class="row">
            <div class="offset-md-1 col-md-2 border border-green"><p>blabla</p></div>
            <div class="col-md-2 border border-green"><p>blabla</p></div>
            <div class="col-md-2 border border-green"><p>blabla</p></div>
            <div class="col-md-2 border border-green"><p>blabla</p></div>
            <div class="col-md-2 border border-green"><p>blabla</p></div>
          </div>
        </div>
      </div>
    </form>
  </div>
</template>
<script>
import axios from 'axios'
export default {
  name: 'app',
  components: {
  },
  data() {
    return {
      resp: null,
      inputdata: "",
      currentTemp: "",
      minTemp:"",
      maxTemp:"",
      sunrise:"",
      sunset:"",
      pressure:"",
      humidity:"",
      wind:"",
      overcast:"",
      icon:"",
      name:""
    }
  },
  methods:{
    getWeather(){
      let url=`http://api.openweathermap.org/data/2.5/weather?q=${this.inputdata}&?units=metric&APPID=386950387b334fecda86df3b8766e7de`;
      axios
        .get(url)
        .then(response => {
          this.resp = response.data;
          this.name = this.resp.name;
          this.currentTemp = this.resp.main.temp;
          this.minTemp = this.resp.main.temp_min;
          this.maxTemp = this.resp.main.temp_max;
          this.pressure = this.resp.main.pressure;
          this.humidity = this.resp.main.humidity + "%";
          this.wind = this.resp.wind.speed + "m/s";
          this.overcast = this.resp.weather[0].description;
          this.icon = "/assets/img/" + this.resp.weather[0].icon.slice(0,2) + ".svg";
          this.sunrise = new Date(this.resp.sys.sunrise*1000).toLocaleTimeString("fr-FR").slice(0.4);
          this.sunset = new Date(this.resp.sys.sunset*1000).toLocaleTimeString("fr-FR").slice(0.4);

        })
      .catch(error => {
        throw(error);
      });
    },
    beforeMonth(){
      this.getWeather();
    }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
