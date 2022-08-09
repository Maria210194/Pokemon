<template>
<div class="container">
    <div class="row ">
        <div class="col-3 fw-bold" v-for="pokemon in filteredPokemons" :key="pokemon.id">
        <PokemonItem :pokemon="pokemon" :imageIndex="pokemon.id" />
        </div>
    </div>

    <div class="row justify-content-center">
        <button @click="goPrevious" class="btn col-6 ms-btn">
            <i class="fa-solid fa-angle-left"></i>
        </button>
        <button @click="goNext" class="btn col-6 ms-btn">
            <i class="fa-solid fa-angle-right"></i>
        </button>

    </div>
</div>
  
</template> 

<script>
import axios from 'axios';
import PokemonItem from '@/components/PokemonItem.vue';

export default {
    name: 'PokemonList',
    components : {
        PokemonItem,
    },
    props: {
        url: String,
        filterByName: String
    },
    data(){
        return{
            pokemons: [], 
            //userò l'offset per mantenere il giusto indice quando navigo tra avanti e indietro
            limit: 898,
            offset: 0, //indice iniziale da cui recuperare i dati, inizialmente valorizzato a 0 perchè parte dalla prima pagina

        }
    },
    // created(){
    //     axios.get(this.url + '?limit=100').then((response)=>{
    //     if(response.status === 200){
    //         console.log('STATUS', response.data);
    //     }
    //     }).catch((error)=>{
    //         console.log('error', error)
    //     })
    // }
    created(){
        this.queryPokemon(this.url);
    },
    computed: {
        filteredPokemons(){
            //aggiungo l'indice all'interno dei nostri oggetti con map; aggiungo poi una nuova proprietà
            //che mi sono inventata, id: index, a cui associo index
            const pokemonsWithId = this.pokemons.map((pokemon, index)=>{
                //uso il destructuring coi 3 punti in modo da spacchettare l'oggetto nei suoi singoli elementi
                //gli sto dicendo di prendere le singole proprietà di pokemon e a queste aggiungere id:index
                return{...pokemon, id: this.offset + index}
            });

            //creo variabile d'appoggio in cui prendo filterByName col lowerCase e trim
            const textToSearch = this.filterByName.toLowerCase().trim();

            //faccio il controllo che textToSearch esista, se non esiste ritorna l'array dei pokemon filtrato con l'id
            if(!textToSearch){
                return pokemonsWithId;
            }

            return pokemonsWithId.filter((pokemon)=>{
                return pokemon.name.toLowerCase().includes(textToSearch);
            })




            /*!!Attenzione, la f.ne scritta così, quando non c'è nessun testo inserito
                torna l'array pokemons senza il filtro che abbiamo implementato

            //creo variabile d'appoggio in cui prendo filterByName col lowerCase e trim
            const textToSearch = this.filterByName.toLowerCase().trim();
                //faccio il controllo che textToSearch esista, se non esiste ritorna l'array dei pokemon
                if(!textToSearch){
                    return this.pokemons
                }
            //filter prende come parametro una f.ne che viene eseguita per ogni item del nostro array(pokemon)
            //se in filter passo solo pokemon, si sballano gli indici che non saranno più quelli originali
            //ma saranno modificati in base al filtro, per evitare ciò, prima di filtrarlo, 
            //aggiungo l'indice all'interno dei nostri oggetti con map; aggiungo poi una nuova proprietà
            //che mi sono inventata, id: index, a cui associo index e poi faccio il filtro
            return this.pokemons.map((pokemon, index)=>{
                return{...pokemon, id:index}
            }).filter((pokemon)=>{
                return pokemon.name.toLowerCase().includes(textToSearch);
            })*/
        }

    },
    methods: {
        //f.ne che riceve un url che utilizzerà per la chiamata
        queryPokemon(url){
            axios.get(url , {
            params: {
                limit: this.limit,
                offset: this.offset
            }
        }).then(({status, data})=>{
            if(status === 200 && data){
                this.pokemons = data.results;
                console.log('response.data: ',data);
                // valorizzo il next e il prev con quelli forniti dall'oggetto(dall'API)
                // this.urlNext = data.next;
                // this.urlPrevious = data.previous;
            }
        }).catch((error)=>{
            console.log('error', error);
        })
        },
        goPrevious(){
            if(this.offset >= this.limit){
                //tolgo xlimit dal numero dell'offset
                this.offset -= this.limit;
                this.queryPokemon(this.url);
            }
        },
        goNext(){
            //aggiungo xlimit al numero dell'offset
            this.offset += this.limit;
            this.queryPokemon(this.url);
        }
    }
}
</script>

 
 <style lang="scss" scoped>
 .container{
    min-height: 85vh;

    .ms-btn{
        width: fit-content;
        margin: 10px 20px;
        border-radius: 50%;
        border: 1px solid white;
        color: white;

    }
 }
 </style>