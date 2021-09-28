<template>
    <h1>Poké-App</h1>
    
    <search-bar 
    v-model="searchQuery"
    ></search-bar>

    

</template>

<script>
import SearchBar from '../components/SearchBar.vue';
import PokemonCard from '@/components/PokemonCard.vue';
import { ref, onMounted, watch } from 'vue';
import axios from 'axios'

export default {
    components: {
        SearchBar,
        
    },

    setup() {
        const searchQuery = ref("");
        const pokemonNames = ref([]);
        

        const getPokemonNames = (url) => {
            axios
                .get(url)
                .then((res) => {
                    res.data.results.forEach((pokemon) => {
                        pokemonNames.value.push(pokemon);
                    })
                    if (res.data.next != null) {
                        return getPokemonNames(res.data.next);
                    }
                });
        }

        const getPokemonByName = (name) => {

        }
        
        onMounted(() => {
            getPokemonNames("https://pokeapi.co/api/v2/pokemon/");
        })

        return {
            pokemonNames,
            searchQuery
        }
    }
    
}
</script>

<style>
body {
    background-color: black !important;
}
</style>