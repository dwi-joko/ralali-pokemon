<template>
  <div id="app">
      <img alt="Vue logo" src="./assets/logo.png">
    <div class="search">
      <input type=" text" v-model="search" placeholder="pokemon name" />
      <span class="dropdown">
      </span>

    </div>
    <div >
      <ul>
        <li v-for="results in filterResults" :key="results" class="tet">
          {{ info }}
          <h2>{{ results.name }}</h2>

          <span class="image">
          </span>

        </li>
      </ul>
    </div>
  </div>
</template>

<script>
import axios from 'axios'

export default {
name: 'App',
data () {
return {
results: [],
search: ''
}
},
mounted() {
axios.get("https://pokeapi.co/api/v2/pokemon/")
.then(response => {this.results = response.data.results})
},
computed:{
filterResults: function(){
return this.results.filter((results) =>{
return results.name.match(this.search);
});
}
}} 
</script>

<style lang="scss">
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
  .search {
    max-width: 25%;
    margin: 0 auto;
    background: #f9f9f9;
    padding: 10px 20px;
    text-align: left;
    input {
        padding: 10px;
        border: 1px solid #eaeaea;
        box-shadow: none !important;
        font-size: 14px;
        width: 100%;
        box-sizing: border-box;
    }
  }
  ul {
    padding: 0;
    background: #f9f9f9;
    li {
        display: inline-block;
        padding: 30px;
        margin: 10px;
        border: 1px solid #eaeaea;
    }
  }
}
</style>
