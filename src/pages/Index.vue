<template>
  <q-page class="fundo">
    <q-card>
      <input type="search" id="address-input" placeholder="Digite a sua cidade" />
    </q-card>
    <q-card v-if="weather && weather.main.temp >= 30" class="card-principal-hot shadow-10">
      <q-card-section class="text-white ">
        <div  class="text-center">
          <span class="text-h6 text-weight-light">{{weather.name}}, </span><small>{{state}}</small>
        </div>
      </q-card-section>
      <q-card-section class="row">
        <div class="col-8">
          <div class="row">
            <div class="col-9 text-right"><span class="text-white ; text-h1 ;text-right">{{parseInt(weather.main.temp)}}</span></div>
            <div class="col-2 text-h4 text-white">ºc</div>
          </div>
        </div>
        <div class="col-4">
          <div class="row text-white">
            <div class="col-12 text-weight-light">Mínima</div>
            <div class="col-12 ">{{parseInt(weather.main.temp_min)}}<small>ºc</small> </div>
            <div class="col-12 text-weight-light">Máxima</div>
            <div class="col-12 ">{{parseInt(weather.main.temp_max)}}<small>ºc</small> </div>
          </div>
        </div>
      </q-card-section>
      <q-card-section class="text-center text-white text-weight-light text-h6 text-capitalize">{{weather.weather[0].description}}</q-card-section>
    </q-card>
    <q-card v-if="weather && weather.main.temp < 30" class="card-principal-cold shadow-10">
      <q-card-section class="text-white ">
        <div  class="text-center">
          <span class="text-h6 text-weight-light">{{weather.name}}, </span><small>{{state}}</small>
        </div>
      </q-card-section>
      <q-card-section class="row">
        <div class="col-8">
          <div class="row">
            <div class="col-9 text-right"><span class="text-white ; text-h1 ;text-right">{{parseInt(weather.main.temp)}}</span></div>
            <div class="col-2 text-h4 text-white">ºc</div>
          </div>
        </div>
        <div class="col-4">
          <div class="row text-white">
            <div class="col-12 text-weight-light">Mínima</div>
            <div class="col-12 ">{{parseInt(weather.main.temp_min)}}<small>ºc</small> </div>
            <div class="col-12 text-weight-light">Máxima</div>
            <div class="col-12 ">{{parseInt(weather.main.temp_max)}}<small>ºc</small> </div>
          </div>
        </div>
      </q-card-section>
      <q-card-section class="text-center text-white text-weight-light text-h6 text-capitalize">{{weather.weather[0].description}}</q-card-section>
    </q-card>
    <div v-if="weather" style="margin-top:50px" class="q-pa-md">
        <div class="row q-col-gutter-x-xs q-col-gutter-y-lg">
          <q-card  class="col-4 bg-green-3">
              <q-card-section>
                <div class="text-weight-light text-white text-center">Umidade</div>
                <div class="text-white text-h4 text-center">{{weather.main.humidity}}%</div>
              </q-card-section>
          </q-card>
          <q-card class="col-4 bg-green-4">
              <q-card-section>
                <div class="text-weight-light text-white text-center">Pressão Atmosférica</div>
                <div class="text-white  text-center">
                  <span class="text-h4 col-12">{{weather.main.pressure}}</span> <small>hPa</small>
                </div>
              </q-card-section>
          </q-card>
          <q-card  class="col-4 bg-green-5">
              <q-card-section>
                <div class="text-weight-light text-white text-center">Ventos</div>
                <div class="text-white  text-center">
                  <span class="text-h4 col-12">{{weather.wind.speed}}</span> <small>km/h</small>
                </div>
              </q-card-section>
          </q-card>
        </div>
    </div>

  </q-page>
</template>

<script>
import axios from 'axios'
// c325cf630346f14f1a73c8210bfeaf64

export default {
  name: 'PageIndex',
  data() {
    return {
      weather: null,
      state: null,
    }
  },
  methods: {
    getWeather(latlng){
      let self = this
      console.log(latlng)
      axios.post('http://api.openweathermap.org/data/2.5/weather?lat='+latlng.lat+'&lon='+latlng.lng+'&appid=c325cf630346f14f1a73c8210bfeaf64&units=metric&lang=pt').then(response => {1
        console.log(response.data);
        self.weather = response.data
      })
    }
  },
  mounted(){
    let self = this
    var places = require('places.js');
    var placesAutocomplete = places({
      appId: "plF695OY2UIM",
      apiKey: "1fb2b7f65223545586176246620e8144",
      container: document.querySelector('#address-input')
    });

    placesAutocomplete.on('change', function(e) {
      self.getWeather(e.suggestion.latlng)
      console.log('SUGESTION')
      self.state = e.suggestion.administrative
    });
  }
}
</script>

<style lang="stylus">
  .fundo{
    background-image: linear-gradient(to bottom right, grey, #dbdbdb)
  }
  .card-principal-hot{
    border-radius: 15px  ;
    margin:20px ;
    padding: 10px ;
    background-color:rgba(255,84,84,0.7)
  }
  .card-principal-cold{
    border-radius: 15px  ;
    margin:20px ;
    padding: 10px ;
    background-color:rgba(57,214,217,0.7)
  }

</style>
