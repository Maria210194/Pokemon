<template>
  <div id="app">
    <HeaderComponent />
    <PokemonList />

  </div>
</template>


<!-- 
    pokemonsURL: "https://pokeapi.co/api/v2/pokemon?limit="

    pokemonImageURL: "https:://raw.githubcontent.com/PokeAPI/sprites/master/sprites/pokemon/other/official-artwork/",
    
    other possible image urls: 
    "https:://raw.githubcontent.com/PokeAPI/sprites/master/sprites/pokemon/{ID}.png"
    "https:://raw.githubcontent.com/PokeAPI/sprites/master/sprites/pokemon/other/official-artwork/{ID}.png"
    "https:://raw.githubcontent.com/PokeAPI/sprites/master/sprites/pokemon/other/home/{ID}.png"<template>
    
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
}
}
</script>

<style lang="scss">
@import '@/styles/general';

</style>
