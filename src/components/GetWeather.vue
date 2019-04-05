<template>
    <form @submit.prevent="getWeather()">
      <div class="row">
        <div class="offset-md-3 col-md-6">
          <div class="form-group">
            <input v-model="inputdata" type="text" class="form-control" aria-describedby="browsecity" placeholder="Enter city">
          </div>
        </div>
      </div>
      <div class="row border-green">
        <div class="offset-md-2 col-md-8 border">
          <div class="row">
            <div class="col-md-12 border">
              <div class="row">
                <div class="col-md-3"><img id="iconeToday" v-bind:src="icon" alt="weather icon"></div>
                <div class="col-md-5"><h1>{{name}}</h1><p>{{currentTemp}}</p></div>
                <div class="col-md-4"><p id="pression">Pression atmosphérique : {{pressure}} pa</p>Humidité : {{humidity}}<p></p>Vent : {{wind}}<p></p></div>
              </div>
            </div>
          </div>
          <div class="row border-green">
            <div class="col-md-3 border"><img class="iconeNext" v-bind:src="icon2" alt="weather icon day 2"><p>{{tomorrowTemp}}</p></div>
            <div class="col-md-3 border"><img class="iconeNext" v-bind:src="icon3" alt="weather icon day 3"><p>{{dayThree}}</p></div>
            <div class="col-md-3 border"><img class="iconeNext" v-bind:src="icon4" alt="weather icon day 4"><p>{{dayFour}}</p></div>
            <div class="col-md-3 border"><img class="iconeNext" v-bind:src="icon5" alt="weather icon day 5"><p>{{dayFive}}</p></div>
          </div>
        </div>
      </div>
    </form>
    </template>
    <script>
    import axios from 'axios'
export default {
  name: 'GetWeather',
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
      icon2:"",
      icon3:"",
      icon4:"",
      icon5:"",
      name:"",
      tomorrowTemp:"",
      dayThree:"",
      dayFour:"",
      dayFive:""

    }
  },
  methods:{
    nextDay(){
      var d = new Date();
      var weekday = new Array(7);
      weekday[0] =  "Sunday";
      weekday[1] = "Monday";
      weekday[2] = "Tuesday";
      weekday[3] = "Wednesday";
      weekday[4] = "Thursday";
      weekday[5] = "Friday";
      weekday[6] = "Saturday";

      var n = weekday[d.getDay()];
    },
    getWeather(){
      axios
        .get("http://api.openweathermap.org/data/2.5/forecast", {
          params: {
            q: this.inputdata,
            units: "metric",
            appid: "2efba0af9e8c46d436bd0cfca1b2df52"
          }
        })
        .then(response => {
          this.resp = response.data.list[0];
          this.resp2 = response.data.list[8];
          this.resp3 = response.data.list[16];
          this.resp4 = response.data.list[24];
          this.resp5 = response.data.list[32];
          this.name = response.data.city.name;
          this.currentTemp = this.resp.main.temp + " C°";
          this.minTemp = this.resp.main.temp_min;
          this.maxTemp = this.resp.main.temp_max;
          this.pressure = this.resp.main.pressure;
          this.humidity = this.resp.main.humidity + " %";
          this.wind = this.resp.wind.speed + " m/s";
          this.tomorrowTemp = this.resp2.main.temp + "C°";
          this.dayThree = this.resp3.main.temp + "C°";
          this.dayFour = this.resp4.main.temp + "C°";
          this.dayFive = this.resp5.main.temp + "C°";
          this.icon = require("../assets/img/" + this.resp.weather[0].icon.slice(0,2) + ".svg");
          this.icon2 = require("../assets/img/" + this.resp2.weather[0].icon.slice(0,2) + ".svg");
          this.icon3 = require("../assets/img/" + this.resp3.weather[0].icon.slice(0,2) + ".svg");
          this.icon4 = require("../assets/img/" + this.resp4.weather[0].icon.slice(0,2) + ".svg");
          this.icon5 = require("../assets/img/" + this.resp5.weather[0].icon.slice(0,2) + ".svg");
        })
      .catch(error => {
        throw(error);
      });
    },

  }
}
    </script>
    <style>
  h1{
    font-weight: bold;
    padding: 5%;
    font-size: 3em;
  }
    #iconeToday{
      width: 150px;
      padding: 10% 0 10% 0;
    }
    .iconeNext{
      width: 100px;
      padding: 10% 0 10% 0;
    }
    #pression{
      padding-top: 10%;
    }
    </style>
    