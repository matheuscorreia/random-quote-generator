<template lang="html">
  <div class="quote">
    <div class="quote__showcase" v-bind:class="{ loading: !isLoading }">
      <div class="quote__text" >
        "{{ quoteText }}"
      </div>
      <div class="quote__author">
        <p> - {{ quoteAuthor }}</p>
      </div>
    </div>
    <div class="quote__buttons">
      <button class="button" v-on:click="getQuote">
        <img class="quote__icon" src="static/icons/rotate-cw.svg" />
      </button>
      <a class="button" v-bind:href="shareURI" target="_blank">
        <img class="quote__icon" src="static/icons/twitter.svg" />
      </a>
    </div>
  </div>
</template>

<script>
import axios from 'axios'

function decodeEntities(str){
  return str.replace(/&#(\d+);/g, function(match, dec) {
    return String.fromCharCode(dec);
  });
}

export default {
  data: function () {
    return {
      quoteText: "",
      quoteAuthor: "",
      isLoading: true,
      shareURI: ""
    }
  },
  methods: {
    getQuote(){
      this.isLoading = false;
      let reqConfig = {
        method: 'get',
        url: 'https://andruxnet-random-famous-quotes.p.mashape.com/?count=1',
        responseType: 'json',
        headers: {
          'X-Mashape-Key': 'rOndnsPdyfmshTaaffz3htkFaLCAp1Cbs23jsnO4hC4WfDmOPc',
          'Accept': 'application/json'
        }
      }

      axios(reqConfig).then(res => {
        let tweet = `"${res.data.quote}" - ${res.data.author}`
        this.shareURI = encodeURI(`https://twitter.com/intent/tweet?text=${tweet}`)
        this.quoteText = res.data.quote
        this.quoteAuthor = res.data.author
        this.isLoading = true;
        this.$emit('changeColor')
      })
    }
  },
  mounted: function () {
    this.getQuote()
  }
}
</script>

<style lang="css" scoped>
div{
  transition: 0.3s all ease-in-out;
}
.quote{
  padding: 100px 50px 0 50px;
  width: auto;
  font-size: 2em;
}

.button {
  background-color: transparent;
  cursor: pointer;
  border: none;
}

.quote__icon{
  position: relative;
  transform: rotate(0deg);
  transition: .5s ease-in-out;
}

.quote__icon:hover{
  transform: rotate(360deg);
}

.quote__author{
  font-size: 0.5em;
}

.quote__showcase.loading{
  filter: blur(10px);
}
</style>
