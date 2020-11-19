<template>
  <div style="display:flex; align-items:center; justify-content:center; flex-direction:column; ">
    <span>{{number + 1}}</span>
    <strong style="color:orangered; align-self:center;">
      {{upper}}
    </strong>
    <small>
      {{url}}
    </small><br>
  </div>
</template>

<script>
import axios from 'axios'
export default {
  
  computed: {

  upper:function(){
      return this.name[0].toUpperCase() + this.name.slice(1)
  },  
  },

    created: async function(){
  
      const response = await axios.get(this.url)
      
      this.pokemon.type = response.data.types[0].type.name
      this.pokemon.front = response.data.sprites.front_default
      this.pokemon.back = response.data.sprites.back_default
        console.log(this.pokemon)
    },

    data(){
      return{
        pokemon:{}

      }

    },
      
  props:{
      name:String,
      url:String,
      number:Number,
  },

}
</script>

<style>

</style>