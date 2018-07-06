<template>
  <div  :class="classChanger()" id="app">
    <weather v-on:changedTemp="updateTemp($event)"></weather>
  </div>
</template>

<script>
import Weather from './components/Weather.vue'

export default {
  name: 'app',
  components: {
    Weather
  },
  data() {
    return {
      temp: "",
    }
  },
  methods: {
    updateTemp(e) {
      this.temp=e;
    },
    classChanger() {
        if (this.temp < 0) {
        return "v-cold";
      } else if (this.temp < 10) {
        return "cold";
      } else if (this.temp < 15) {
        return "mild";
      } else if (this.temp < 20) {
        return "warm";
      } else if (this.temp < 25) {
        return "hot";
      } else if (this.temp < 30) {
        return "v-hot";
      } else if (this.temp >= 30) {
        return "v-hot";
      }
    }
  }
}
</script>

<style>
#app {
  font-family: 'Montserrat', sans-serif;
  padding-top: 60px;
  padding-bottom: 60px;
  height: 450px;
}
.v-cold {
  background: #c0c0aa;  /* fallback for old browsers */
  background: -webkit-linear-gradient(to bottom, #1cefff, #c0c0aa);  /* Chrome 10-25, Safari 5.1-6 */
  background: linear-gradient(to bottom, #1cefff, #c0c0aa); /* W3C, IE 10+/ Edge, Firefox 16+, Chrome 26+, Opera 12+, Safari 7+ */


}

.cold {
  background: #c2e59c;  /* fallback for old browsers */
background: -webkit-linear-gradient(to bottom, #64b3f4, #c2e59c);  /* Chrome 10-25, Safari 5.1-6 */
background: linear-gradient(to bottom, #64b3f4, #c2e59c); /* W3C, IE 10+/ Edge, Firefox 16+, Chrome 26+, Opera 12+, Safari 7+ */


}

.mild {

  background: #dce35b; /* fallback for old browsers */
  background: -webkit-linear-gradient(to bottom, #dce35b, #45b649); /* Chrome 10-25, Safari 5.1-6 */
  background: linear-gradient(to bottom, #dce35b, #45b649); /* W3C, IE 10+/ Edge, Firefox 16+, Chrome 26+, Opera 12+, Safari 7+ */


}
.warm {
  background: #FF5F6D;  /* fallback for old browsers */
background: -webkit-linear-gradient(to bottom, #FFC371, #FF5F6D);  /* Chrome 10-25, Safari 5.1-6 */
background: linear-gradient(to bottom, #FFC371, #FF5F6D); /* W3C, IE 10+/ Edge, Firefox 16+, Chrome 26+, Opera 12+, Safari 7+ */


}
.hot {
  background: #FF4E50;  /* fallback for old browsers */
background: -webkit-linear-gradient(to bottom, #F9D423, #FF4E50);  /* Chrome 10-25, Safari 5.1-6 */
background: linear-gradient(to bottom, #F9D423, #FF4E50); /* W3C, IE 10+/ Edge, Firefox 16+, Chrome 26+, Opera 12+, Safari 7+ */


}
.v-hot {
  background: #c21500;  /* fallback for old browsers */
background: -webkit-linear-gradient(to bottom, #ffc500, #c21500);  /* Chrome 10-25, Safari 5.1-6 */
background: linear-gradient(to bottom, #ffc500, #c21500); /* W3C, IE 10+/ Edge, Firefox 16+, Chrome 26+, Opera 12+, Safari 7+ */


}
</style>
