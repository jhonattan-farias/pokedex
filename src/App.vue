<template>
<div>
  <div class="logo">
  <img src="https://vibrant-yonath-715bf2.netlify.app/static/media/pokedex-logo.dc5fe4c4.svg" alt="">
  </div>

  <div class="inp">
  <input type="text" v-model="pokeName" placeholder="Digite o nome do pokemon">
  </div>

<div id="app" v-for="(pokemon,index) in check" :key="pokemon.name">

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

        pokemons : [],
        filteredPokemon:[],
        pokeName:'',

      }
    },

  created: async function(){
    const response = await axios.get("https://pokeapi.co/api/v2/pokemon?limit=151&offset=0")

    console.log("Pokemons capturados")

    this.pokemons = response.data.results

    console.log(this.pokemons)
  },

  computed:{
    check: function(){
     if(this.pokeName === ''){
       return this.pokemons
     } 

    return this.pokemons.filter(poke=> poke.name.search(this.pokeName) > -1)
     
     
    }
  }

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
}

.logo img{
  width:300px ;
}

.inp{
  display: flex;
  justify-content: center;
  background: rgba(255, 115, 0, 0.733) ;
  height: 80px;
}
input{
  height: 60px;
  width:450px ;

  border: none;
  outline: none;
  border-radius:10px;
  padding: 1rem;

  font-family:Lato;
  font-weight: bold;
  font-size: 12pt;


}
</style>
