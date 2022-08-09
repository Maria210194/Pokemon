<template>
  <div>
    <div class="d-flex justify-content-between ms-header">
      <div class="d-flex">
        <img class="ms-pokeball" src="@/assets/ball.png" alt="">
        <p>Pokédex</p>
      </div>
      <div class="mx-3">
        <input
        type="text"
        v-model="searchedPokemon"
        @keyup="search"
        placeholder="Cerca un pokemon.."
        class="ms-input">
      </div>
    </div>
  </div>
</template>

<script>
export default {
    name: 'HeaderComponent', 
    data(){
      return {
        searchedPokemon: ''
      }
    },
    methods: {
      search(){
        console.log(this.searchedPokemon);
        this.$emit('nomeEvento', this.searchedPokemon);
      }
    }

}
</script>


<style lang="scss" scoped>
.ms-header{
  padding: 10px;
  margin-bottom: 20px;
  background: linear-gradient(90deg, #0E273C,  #22181C) ;
  color: white;

  .ms-pokeball{
    width: 45px;
  }

  p{
    font-size: 1.2rem;
    margin: 0 !important;
    align-self: center;
    padding: 5px 10px;
  }
  
  .ms-input{
    vertical-align: -webkit-baseline-middle;
    font-size: 0.9rem;
    margin: 10px;

  }

  .ms-button{
    max-height: 35px;
    vertical-align: -webkit-baseline-middle;
    .img-button{
          max-width: 25px;
          filter: invert;
    }
  }
}
</style>