<template>
  <div class="column is-half is-offset-one-quarter">
    <h4 class="is-size-4">PokéDex</h4>
    <input type="text" placeholder="Buscar pelo nome..." v-model="busca" class="input is-rounded">
    <button class="button is-fullwidth is-success" id="busca-btn" @click="buscar">Buscar</button>
    <div v-for="(pokemon, index) in filteredPokemons" :key="pokemon.url">
      <Pokemon 
        :name="pokemon.name"
        :url="pokemon.url"
        :num="index + 1"
      />
    </div>
  </div>
</template>

<script>
import axios from 'axios';
import Pokemon from './components/Pokemon';

export default {
  name: 'App',
  data(){
    return {
      pokemons: [],
      filteredPokemons: [],
      busca: ""
    }
  },

  // created (tem que ser essa) => ai chamar os dados sempre que for carregado
  created: function(){
    axios.get('https://pokeapi.co/api/v2/pokemon?limit=151&offset=0').then(res => {
      this.pokemons = res.data.results;
      this.filteredPokemons = res.data.results;
      console.log("Pegou a lista de Pokémons");
    });
  },
  components: {
    Pokemon
  },
  methods: {
    buscar: function(){
      this.filteredPokemons = this.pokemons;
      if(this.busca == '' || this.busca == ' '){
        this.filteredPokemons = this.pokemons;
      }else{
        this.filteredPokemons = this.pokemons.filter(pokemon => pokemon.name.toUpperCase() == this.busca.toUpperCase());
      }
    }
  },
  computed: {
    /* Busca sem botão
    resultadoBusca: function(){
      if(this.busca == '' || this.busca == ' '){
        return this.pokemons;
      }else{
        return this.pokemons.filter(pokemon => pokemon.name.toUpperCase() == this.busca.toUpperCase());
      }
    }
    */

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

#busca-btn {
  margin-top: 5px;
}
</style>
