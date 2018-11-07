<template>
  <div class="home">
        <div class="row">
        <div class="input-group mb-3">
          <input v-model="location" type="text" class="form-control" placeholder="Enter city name e.g. 'London'">
          <div class="input-group-append">
            <button
              @click="updateLocation"
              class="btn btn-outline-secondary"
              type="button">Search</button>
          </div>
        </div>
      </div>
  <div class="row">
  <div class="card text-white bg-info mb-3 col-sm-12 col-lg-2" v-for="day in 5" :key='day.id' v-if="forecast">
    <div class="card-header">Forecast for {{forecast.city.name}}</div>
    <div class="card-body">
      <h4 class="card-title">{{forecast.list[day].weather[0].description}}</h4>
      <p class="card-text"><img v-bind:src="`https://openweathermap.org/img/w/${forecast.list[day].weather[0].icon}.png`"><br>
      </p>
      <p class="card-text">{{forecast.list[day].main.temp}}&deg;
      </p>
    </div>
  </div>
</div>
  </div>
</template>

<script>
import API from '@/lib/API';

export default {
  name: 'home',
  data() {
    return {
      location: '',
      forecast: null
    }
  },
  mounted() {
    var self = this;
    API.getForecast()
    .then(result => {
      this.forecast = result;
    })
    window.addEventListener('keyup', function(event){
      if (event.keyCode === 13) {
        self.updateLocation()
      }
    })
  },
methods: {
    loadWeather(lat, lng) {
      API.getForecast(lat, lng).then((result) => {
        this.forecast = result;
      });
    },
    updateLocation() {
      API.getCoordinatesFromCityName(this.location).then((result) => {
        this.loadWeather(result.list[0].coord.lat, result.list[0].coord.lon);
      });
    },
  },
};
</script>

<style lang="scss">
$im-a-contrived-variable-name: inherit;
.card-title {
  color: $im-a-contrived-variable-name;
}
</style>
