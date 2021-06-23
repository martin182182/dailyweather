<template>
  <div class="row">
    <h4>Bienvenido/a</h4>
    <select id="cities">
      <option class="op" id="ambato" value="ambato">Ambato</option>
      <option class="op" id="quito" value="quito">Quito</option>
      <option class="op" id="riobamba" value="riobamba">Riobamba</option>
      <option class="op" id="latacunga" value="latacunga">Latacunga</option>
      <option class="op" id="guayaquil" value="guayaquil">Guayquil</option>
    </select>
    <br><br>
    <button v-on:click="weather()">Ver clima</button>
    <br><br>
    <div class="card">
      <img src="" id="img1"> 
      <h5>Ciudad:</h5>
       <h5>{{cityModel.city}}</h5>
      <h5>Temperatura:</h5>
      <h5>{{cityModel.temp}}</h5>
      <h5>Descripcion</h5>
      <h5>{{cityModel.description}}</h5>
      <h5>Presion</h5>
      <h5>{{cityModel.pressure}}</h5>
      <h5>Humedad</h5>
      <h5>{{cityModel.humidity}}</h5>
    </div>
  </div>
</template>
<script>
import axios from 'axios';
export default {
  data(){
    return {
      url: 'https://api.openweathermap.org/data/2.5/weather?q=',
      cityData: '',
      cityModel: {
        city: '',
        temp: 0,
        description: '',
        pressure: 0,
        humidity: 0,
        icon: ''
      }
    }
  },
  methods:{
    weather(){
      var city = document.getElementById("cities").value;
      this.cityModel.city = city.toUpperCase();
      axios.get(this.url+city+'&appid=44da42bc69db778b5309726d3d9d8b29')
      .then(res=>{
        this.cityData = res.data;
        this.cityModel.temp = this.cityData["main"].temp-273.15;
        this.cityModel.description = this.cityData["weather"][0].description;
        this.cityModel.pressure = this.cityData["main"].pressure;
        this.cityModel.humidity = this.cityData["main"].humidity;
        this.cityModel.icon = this.cityData["weather"][0].icon;
        document.getElementById("img1").src="https://openweathermap.org/img/wn/"+this.cityModel.icon+"@2x.png";
      })
      .catch(e=>console.log(e));
    }
  }
}
</script>
<style>
  h4{
    font-size: 48px;
    font-weight: 700;
    color: rgba(33, 11, 61, 0.788);
  }
  select{
    width: 200px;
    height: 50px;
    border: none;
    border-bottom: 2px solid rgba(33, 11, 61, 0.788);
  }
  .op{
    font-size: 24px;
  }
  .card{
    width: 400px;
    height: auto;
    border: 2px solid rgba(33, 11, 61, 0.788);
    margin-left: auto;
    margin-right: auto;
  }
</style>
