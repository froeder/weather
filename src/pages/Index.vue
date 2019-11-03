<template>
  <q-page class="bg-grey-3">
    <q-card>
      <input type="search" id="address-input" placeholder="Digite a sua cidade" />
    </q-card>

    <q-card class="shadow-10 card-temp" v-if="weather"
      style="
        margin:20px ;
        border-radius:10px;
        background-image: linear-gradient(to bottom right, #00e6c7, #21d3ff);"
    >

      <q-card-section>
        <div class="text-h6 text-center text-white text-weight-light">{{weather.name}}</div>
        <div style="margin-top:15px" class="text-h2 text-center">
        {{weather.main.temp}}  <span style="font-size:.5em ; marginBottom:20px;paddingBotto:30px">ºc</span>

        </div>
        <div class="text-center text-h6 text-capitalize">
          {{weather.weather[0].description}}
        </div>
      </q-card-section>
    </q-card>

    <div v-if="weather" class="q-pa-md">
       <div class="row q-col-gutter-x-xs">
        <q-card class="col-6 text-center"
          style="background-image:linear-gradient(to bottom right, #2036c7, #36ffd7)"
        >
          <q-card-section>
            <div class="text-weight-light">Mínima</div>
            <div class="text-h5">{{weather.main.temp_min}}<span style="font-size:.8em">ºc</span></div>
          </q-card-section>
        </q-card>
        <q-card class="col-6 text-center"
          style="background-image:linear-gradient(to bottom right, #ff5454, #ffdd00)">
          <q-card-section>
            <div class="text-weight-light">Máxima</div>
            <div class="text-h5">{{weather.main.temp_max}}<span style="font-size:.8em">ºc</span></div>
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
      weather: null
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
      self.getWeather(e.suggestion.latlng) ;
    });
  }
}
</script>
