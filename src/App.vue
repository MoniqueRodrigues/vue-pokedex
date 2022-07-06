<template>  



       <input type="text" v-model="search" placeholder="Search" >    
    <div class="container">     
     

      <ul>
        <li class="card" v-for="pokemon, idx in filter_pokemons"
          :key="pokemon.name" >         
        
            <img 
                :src="`https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/${get_id(pokemon)}.png`"
                :alt="pokemon.name"                                
            />        
                    
          <p class="poke-names">{{pokemon.name}}</p>
          <p class="poke-id"> #{{idx + 1}}</p>
          
        </li>            
      </ul>
        
    </div>
</template>

<script>      
      import axios from "axios";

      export default {
        name: "App",

        components:{},

        data() {
          return {
            pokemons:[],
            search: "",         
          }
        },

        computed:{
          filter_pokemons(){
            return this.pokemons.filter(pokemon=> !pokemon.name.indexOf(this.search))
          }
        },
        
        mounted(){
            axios
              .get("https://pokeapi.co/api/v2/pokemon?limit=151")
              .then((response)=>  {
                console.log(response)
                this.pokemons = response.data.results
              });        

          },

          methods:{
            get_id(pokemon){
              return pokemon.url.split("/")[6]
            }       
          }
      }
      
      
   </script>
  


  




