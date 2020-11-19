<template>
  <div class="all" style="display:flex; align-items:center; justify-content:center; ">
    <strong style="margin-right:5px; color:white;">{{number}}</strong>

    <div class="pokemon">
      <div class="img">
        
        <img  @click="changeImg" :src="pokeImg">
        <p>Clique</p>
      </div>
      <div class="info">

        <div class="name">
         <strong>{{name}}</strong>
        </div>

        <div class="type">
          <p>{{pokemon.type}}</p>
        </div>

      </div>
    </div>
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
      
      this.pokeImg = this.pokemon.front
    },

    data(){
      
      return{
        pokemon:{
          type:'',
          front:'',
          back:'',
          },
          pokeImg:'',
          
      }
      

    },
      methods:{

      changeImg: function(){

        var front = this.pokemon.front
        var back = this.pokemon.back

        if(this.pokeImg === front){
        this.pokeImg = back
        }
        else{
         this.pokeImg = front
        }

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

.all{
  background: rgb(235, 235, 235);
}

.pokemon{
  transition:.2s;
  cursor: pointer;
  width: 250px;
  padding-bottom: 10px;
}
.pokemon:hover{
transform: translateX(15px);
}

.img{
  text-align: center;
  background: rgb(234, 246, 248);
  border-radius: 10px 10px 0 0;
  margin-top: 10px;
  width:250px;
  padding-bottom: 10%;

}

img{
width: 150px;
height: 150px;

margin-top: 2%;
}

.info{
  display: flex;
  flex-direction: column;
  align-items: center;

  background:#8CEBA2;
  border-radius: 0 0 10px 10px;
  padding: .5rem;
}


strong{
  font-family: Lato;
  font-size: 20pt;
  color: #39486B ;
  font-weight: bold ;
}

.type{
  display: flex;
  justify-content: center;

  background: white;
  width:70px;
  border-radius:20px;

  margin-top: 10px;
  height: 25px;
}
p{
  font-family: Lato;
  font-weight: 400;
  font-size: 13pt;
}
</style>