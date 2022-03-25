<template>
  <q-page class="flex flex-center">
     <div
       :class="typeof weather.main != 'undefined' && weather.main.temp >= 16 ? 'bg-img-rain' : 'bg'"
      > 
      <div class="back-blur">
         <div class="absolute-top text-subtitle1 text-center">
           <q-input
              v-model="search"
              label="Search"
              color="blue"
              label-color="blue"
              filled
              dark
              @keypress.enter="searchWeather"
              class="relative q-ma-lg"
      >
    </q-input>
         </div>
         <div  v-if="typeof weather.main != 'undefined' " class="absolute-center  text-center">
           <q-card dark bordered class="bg-transparent my-card">
            <q-card-section>
              <div class="text-h2">{{weather.name}}, {{weather.sys.country}}</div>
              <div class="text-h2 q-mt-md">{{Math.round(weather.main.temp)}} ^C</div>
            </q-card-section>
          <q-separator dark inset />
      <q-card-section class="text-h3">
        {{weather.weather[0].main}}
      </q-card-section>
           </q-card>
         </div>
      </div>
      </div>
  </q-page>
</template>

<script>
import { defineComponent } from 'vue';

export default defineComponent({
  name: 'PageIndex',
  data(){
    return{
      api_key: '076a814af8c08bafa4fe1b7ec2fb2385',
      url_base: 'https://api.openweathermap.org/data/2.5/',
      search: 'Ferghana',
      weather: {},
      img: ''
    }
  },
  methods:{
    searchWeather(){
      fetch(`${this.url_base}weather?q=${this.search}&units=metric&appID=${this.api_key}`)
      .then(res=>{
        return res.json()
      })
      .then(
        this.result,
      )
    },
    result(results){
      this.weather = results
      
    },
  
  }
})
</script>
<style scoped>
.my-card{
  width: 500px;
  height: 40%  
}
.bg-img-rain{
  width: 100%;
  height: 93vh;
  background-image: url('https://static.vecteezy.com/system/resources/previews/001/740/998/large_2x/rain-drops-on-the-window-with-colorful-bokeh-free-photo.jpg' );
  background-color: #000000;
  background-size: cover;
 
 
}
.bg{
    width: 100%;
  height: 93vh;
  background-image: url('https://static.vecteezy.com/system/resources/previews/003/512/413/large_2x/dramatic-sky-with-stormy-clouds-free-photo.jpg' );
  background-color: #000000;
  background-size: cover;
}
.back-blur{
   background: rgba(255, 255, 255, 0.2);
  backdrop-filter: blur(6px); 
  height: 93vh;
  width: 100%;
}
</style>