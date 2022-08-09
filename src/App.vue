<template>
  <div id="app">
    <HeaderComponent @nomeEvento="doSearch"/>
    <PokemonList :url="pokemonsURL" :filterByName="searchPokemon" />

  </div>
</template>


<!-- 
    pokemonsURL: "https://pokeapi.co/api/v2/pokemon"

    pokemonImageURL: "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/official-artwork/",
    
    other possible image urls: 
    "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/{ID}.png"
    "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/official-artwork/{ID}.png"
    "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/home/{ID}.png"
    
    pokemonURL: "https://pokeapi.com/api/v2/pokemon/"
-->

<script>
import HeaderComponent from '@/components/HeaderComponent.vue';
import PokemonList from './components/PokemonList.vue';



export default {
  name: 'App',
  components: {
    HeaderComponent,
    PokemonList
  },
  data(){
    return {
          pokemonsURL: "https://pokeapi.co/api/v2/pokemon",
          searchPokemon: ''
    }
  },
  methods: {
    doSearch(text){
      console.log('App.vue --> ', text);
      //associo a searchPokemon che ho in data il valore text
      this.searchPokemon = text;
    }
  }
}
</script>

<style lang="scss">
@import '@/styles/general';
#app{
   background-color: #ff8906;
}

</style>
