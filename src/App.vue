<template>
  <div id="app">
    <HeaderComponent />
    <PokemonList />

  </div>
</template>

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
