<template>
    <div class="card my-2 mx-2 ms-card">
        <img :src="pokemonImageUrl" :alt="pokemon.name" />
        <p class="text-center my-2 text-uppercase">
            {{pokemon.name}}
        </p>
    </div>
</template>

<script>
export default {
    name: 'PokemonItem', 
    props: {
        pokemon : Object,
        imageIndex: Number,
    },
    data(){
        return {
            imageUrlBase : "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/official-artwork/"
        }
    },
    //col mounted posso osservare che mi tornarà un pokemon diverso dall'originale
    //con la proprietà id che ho appena assegnato in PokemonList:
    mounted() {
        console.log(this.pokemon);
        //es risultato Console: {name: 'voltorb', url: 'https://pokeapi.co/api/v2/pokemon/100/', id: 99}
    },
    computed: {
        pokemonImageUrl(){
            return this.imageUrlBase + (this.imageIndex + 1) + '.png'
        }
    }
}
</script>

<style lang="scss" scoped>
.ms-card{
    img{
        filter: drop-shadow(2px 4px 6px black);
        padding: 0.1rem;
        opacity: 0.8;
    &:hover{
        opacity: 1;
        scale: 1.3;
    }}

    p{
        font-size: 0.7rem;
    }
    
}

</style>