<template>
  <div class="column is-half is-offset-one-quarter">
    <h1 class="is-size-1">Pokedex</h1>

    <input class="input is-rounded" type="text" placeholder="Buscar Pokemon pelo nome" v-model="busca">
    <button class="button is-success" @click="buscar">Buscar</button>

    <div v-for="(poke, index) in filteredPokemons" :key="poke.url">
        <Pokemon :name="poke.name" :url="poke.url" :num="index + 1"/>
    </div>
  </div>
</template>

<script>
import  axios from 'axios';
import Pokemon from './components/Pokemon.vue';

export default {
  name: 'App',
  data(){
    return{
      filteredPokemons:[],
      pokemons:[],
      busca:''
    }
  },
  created: function(){
    axios.get('https://pokeapi.co/api/v2/pokemon?limit=151&offset=0').then(res =>{
      // console.log(res.data.results);
      this.pokemons = res.data.results;
      this.filteredPokemons = res.data.results;
    })
  },
  components:{
    Pokemon
  },
  methods:{
    buscar: function(){
      this.filteredPokemons = this.pokemons;
      if(this.busca === '' || this.busca === ' '){
        this.filteredPokemons = this.pokemons;
        }else{
          this.filteredPokemons = this.pokemons.filter(pokemon => pokemon.name == this.busca);
        }
    }
  },
 computed:{
  //   resultadoBusca: function(){
  //     if(this.busca === '' || this.busca === ' '){
  //       return this.pokemons;
  //     }else{
  //       return this.pokemons.filter(pokemon => pokemon.name == this.busca);
  //     }
  //   }
 }

}
</script>

<style>
#app {
  text-align: center;
}
.button{
  width: 50%;
  margin-top: 10px;
}
</style>
