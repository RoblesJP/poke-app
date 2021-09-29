<template>
    <h1>Poké-App</h1>
    
    <search-bar 
    v-model="searchQuery"
    ></search-bar>

    <pokemon-card
    v-if="pokemon"
    :imageURL="pokemon.sprites.front_default"
    ></pokemon-card>

</template>

<script>
import SearchBar from '../components/SearchBar.vue';
import PokemonCard from '@/components/PokemonCard.vue';
import { ref, onMounted, watch } from 'vue';
import axios from 'axios'

export default {
    components: {
        SearchBar,
        PokemonCard
    },

    setup() {
        let url = "https://pokeapi.co/api/v2/pokemon/";
        const searchQuery = ref("");
        const pokemonNames = ref([]);
        const pokemon = ref(null);
        

        const getPokemonNames = (url) => {
            axios
                .get(url)
                .then((res) => {
                    res.data.results.forEach((pokemon) => {
                        pokemonNames.value.push(pokemon.name);
                    })
                    if (res.data.next != null) {
                        return getPokemonNames(res.data.next);
                    }
                });
        }

        const getPokemonByName = () => {
            let name = searchQuery.value;
            if (name != null && name !== "" && pokemonNames.value.includes(name)) {
                axios
                .get(url + name)
                .then(res => pokemon.value = res.data);
                console.log("request for " + name);
            }
            
        }
        
        onMounted(() => {
            getPokemonNames(url);
        });

        watch(searchQuery, getPokemonByName);

        return {
            pokemonNames,
            searchQuery,
            pokemon
        }
    }
    
}
</script>

<style>
body {
    background-color: black !important;
}
</style>