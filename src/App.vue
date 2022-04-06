<template>
  <div>
    <h1>First project with D3 and Vue.js</h1>
    <p>{{numbers}}</p>
    <button @click="shuffleNumbers()">Shuffle</button>
  </div>
</template>

<script>
const d3 = require('d3');

export default {
  name: 'App',
  components: {
  },
  data: function() {
    return {
      numbers:[2,4,7,8,13],
    };
  },
  methods:{
    shuffleNumbers: function(){
      this.numbers = d3
              .range(Math.round(Math.random() * 20))
              .map(() => Math.round(Math.random() * 100))
    }
  }

}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
