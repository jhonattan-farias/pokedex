<template>
<div>
  <div class="logo">
  <img src="https://vibrant-yonath-715bf2.netlify.app/static/media/pokedex-logo.dc5fe4c4.svg" alt="">
  </div>
<div id="app" v-for="(pokemon,index) in pokemons" :key="index">

  <Pokemon :name="pokemon.name" :url="pokemon.url" :number="index"/>
</div>
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
*{
  padding: 0;
  margin: 0;
  box-sizing:border-box;
}
#app{
}
div.logo{
  background: rgba(255, 115, 0, 0.733);
  width:100%;
  display: flex;
  justify-content: center;
  align-items: center;
}

.logo img{
  width:300px ;
}
</style>
