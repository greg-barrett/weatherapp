<template>
  <div class="main">
    <input placeholder="City Name" v-model="town" v-on:keyup.enter="getWeather" v-on:keyup.backspace="clearAll" >
    <transition name="alert-in" enter-active-class="animated flipInX" leave-active-class="animated flipOutX">
      <div v-show="shown" class="forecast">
        <p>{{town}}</p>
        <p>{{description}}</p>
        <i class="icon" v-bind:class="icon" ></i>
        <p  v-on:click="tempCon">Today's High: {{high.toFixed(0)}}<span v-show="metric"> &#8451;</span><span v-show="!metric"> &#8457;</span></p>
      </div>
    </transition>
    <p class="error" v-show="!shown">{{error}}</p>
  </div>
</template>

<script>
let iconMap= {
    "wi-owm-200": "Thunderstorm",
    "wi-owm-210": "Lightning",
    "wi-owm-300": "Drizzle",
    "wi-owm-302": "Rain",
    "wi-owm-313": "Showers",
    "wi-owm-531": "Storm-showers",
    "wi-owm-600": "Snow",
    "wi-owm-602": "Sleet",
    "wi-owm-711": "Smoke",
    "wi-owm-731": "Dust",
    "wi-owm-741": "Fog",
    "wi-owm-781": "Tornado",
    "wi-owm-800": "Clear",
    "wi-owm-804": "Clouds",
    "wi-owm-902": "Hurricane",
    "wi-owm-904": "Hot",
    "wi-owm-905": "Windy",
    "wi-owm-906": "Hail",
}

export default {
  name: 'Weather',
  props: {
    temp: {
      type:String
    }
  },

  data () {
    return {
      town: "",
      data:"",
      description:"",
      high:0,
      shown: false,
      error:"",
      metric:true,
      symbol:"C",
      icon:""
    }
  },
  methods: {
    sendTemp() {
      this.$emit("changedTemp", this.high)
    },
    clearAll(){
      this.shown= false;
    },
    capitalizeFirstLetter() {
       this.town= this.town.charAt(0).toUpperCase() + this.town.slice(1);
     },
    getIcon() {
      for (var key in iconMap) {
        if (iconMap[key]===this.description) {
          this.icon="wi "+ key;
          return
        }

      }
    },
    async getWeather() {
      this.capitalizeFirstLetter();
      try {
        let response= await fetch('https://api.openweathermap.org/data/2.5/weather?q='+ this.town +'&APPID=eb298f5202793a5a6f90604be2e29842&units=metric');
        let data= await response.json();
        if (data.cod=="200") {
           this.data=data;
           this.description=data.weather[0].main;
           this.high=data.main.temp;
           this.shown=true;
           this.metric=true;
           this.getIcon();
           this.sendTemp();
         } else {
           this.error="Huston we have a problem";
           this.shown=false;
         }

      } catch(error) {
        console.log(error);
      }
    },
    tempCon() {
      if (this.metric) {
        this.high=(this.high *1.8) +32
        this.metric=false;
      } else {
        this.high=(this.high-32)/1.8
        this.metric=true;
      }
    }
  }
}

</script>
<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
@import "https://cdn.jsdelivr.net/npm/animate.css@3.5.1";
.main {
  width: 400px;
  margin: auto;
  height: 400px;
  background-color: white;
  border-radius: 20px;
  text-align: center;
  box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2);

}
input {
  width: 40%;
  margin-top: 40px;
  text-align: center;
  font-size: 1.2em;
  border: none;
  border-bottom: 3px solid gray;
  padding-bottom: 5px;
}

.forecast {
  text-align: center;
  font-size: 1.5em;

}
.icon {
  font-size: 4em;

}
.error {
  text-align: center;
  padding-top: 50px;
}

@media only screen and (max-width: 480px) {
  .main {
    width: 80%;
  }
  input {
    width: 80%;
  }
}
@media only screen and (max-width: 720px) {
  .main {
    width: 60%;
  }

}


</style>
<style src="../../css/weather-icons.css"></style>
