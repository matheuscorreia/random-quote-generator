<template>
  <div id="app" v-bind:style="{'background-color':`rgba(${color.r}, ${color.g}, ${color.b}, ${color.a})`}">
    <div class="header">
      <span class="header__text">random</span>
      <img src="static/icons/feather.svg" class="header__icon" />
      <span class="header__text">quote</span>
    </div>
    <quote v-on:changeColor="randomColor"></quote>
  </div>
</template>

<script>
import Quote from './components/Quote.vue';

function randomBetween(min, max){
  return Math.ceil(Math.random() * (max - min) + min);
}

export default {
  name: 'app',
  components: {
    'quote': Quote
  },
  data: function () {
    return {
      color: {
        r: 0,
        g: 0,
        b: 0,
        a: 0.5,
      }
    }
  },
  methods: {
    randomColor(){
      this.color.r = randomBetween(0,255);
      this.color.g = randomBetween(0,255);
      this.color.b = randomBetween(0,255);
    }
  }
}
</script>

<style>
#app{
  height: 100%;
  transition: 1s all ease-in-out;
}
html, body {
  margin: 0;
  padding: 0;
  height: 100%;
}
html {
  background: url('/static/img/bg.png');
  background-repeat: repeat;
  font-family: 'Raleway';
}
.header__text{
  margin: 0 auto;
  font-size: 3em;
  font-weight: 300;
  padding: 20px 0px 0px 20px;
}
.header__icon{
  margin: 0px 0px 0px 20px;
}
</style>
