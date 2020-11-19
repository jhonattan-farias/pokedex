<template>
<div id="app" v-for="(pokemon,index) in pokemons" :key="index">
  <Pokemon :name="pokemon.name" :url="pokemon.url" :number="index"/>
</div>
</template>

<script>
import axios from 'axios'
import Pokemon from './components/Pokemon';

export default {
  name: 'App',
  components: {
    Pokemon
    },

    data(){
      return{
        pokemons : []
      }
    },

  created: async function(){
    const response = await axios.get("https://pokeapi.co/api/v2/pokemon?limit=151&offset=0")

    console.log("Pokemons capturados")

    this.pokemons = response.data.results

    console.log(this.pokemons)
  },

  }
</script>

<style>
#app {

}
</style>
