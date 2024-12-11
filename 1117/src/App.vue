<script>
import axios from "axios";
export default {
   data(){
      return{
        city: '',
        error: '',
        info: null
      }
   },
  computed: {
     cityName (){
       return '<' + this.city + '>'
     },
    showTemp(){
       return 'Temperature:' +this.info.main.temp
    },
    showFeelsLIke(){
      return 'Feel like:' +this.info.main.feels_like
    },
    showMinTemp(){
      return ' Min. temperature:' +this.info.main.temp_min
    },
    showMaxTemp(){
      return 'Max. temperature:' +this.info.main.temp_max
    },


  },
  methods:{
     getWeather(){
       if(this.city.trim().length < 2){
         this.error = 'The name must be more than one character.'
         return false
       }
       this.error = ''

       axios.get(`https://api.openweathermap.org/data/2.5/weather?q=${this.city}&units=metric&appid=3d9de74844d28377e81415151cbe6a66`)
           .then(res => (this.info = res.data))
     }
  }
}
</script>

<template>
  <div class="wrapper">
    <h1>A weather application</h1>
    <p>Find out the weather in  {{city == '' ? ' your city.' : cityName}}</p>
    <input type="text"  v-model="city" placeholder="Enter the city.">
    <button v-show="city != '' " @click="getWeather()">Enter</button>
    <p class="error">{{error}}</p>

    <div v-if="info != null">
      <p>{{showTemp}}</p>
      <p>{{showFeelsLIke}}</p>
      <p>{{showMinTemp}}</p>
      <p>{{showMaxTemp}}</p>
    </div>

  </div>
</template>



<style scoped>



.wrapper .error{
  color: red;
}

.wrapper{
  width: 900px;
  height: 500px;
  border-radius: 50px;
  padding: 20px;
  background: #2c3e50;
  text-align: center;
  h1{
    color: white;
    margin-top: 50px;
  }
  p{
    color: white;
    margin-top: 20px;
  }
  input{
    margin-top: 30px;
    background: transparent;
    border: 0;
    border-bottom: 2px solid blue;
    color: white;
    font-size: 14px;
    padding: 5px 8px;
    outline: none;
  }
  button{
    width: 100px;
    --b: 3px;
    --s: .45em;
    --color: white;
    margin: 10px;
    padding: calc(.5em + var(--s)) calc(.9em + var(--s));
    color: var(--color);
    --_p: var(--s);
    background:
        conic-gradient(from 90deg at var(--b) var(--b),#0000 90deg,var(--color) 0)
        var(--_p) var(--_p)/calc(100% - var(--b) - 2*var(--_p)) calc(100% - var(--b) - 2*var(--_p));
    transition: .3s linear, color 0s, background-color 0s;
    outline: var(--b) solid #0000;
    outline-offset: .6em;
    font-size: 16px;
    border: 0;
    user-select: none;
    -webkit-user-select: none;
    touch-action: manipulation;
  }
}


.wrapper button:hover,
.wrapper button:focus-visible{
  --_p: 0px;
  outline-color: var(--color);
  outline-offset: .05em;
}

.wrapper button:active {
  background: var(--color);
  color: #fff;
}


.wrapper input:focus{
  border-bottom-color: white;
}



</style>
