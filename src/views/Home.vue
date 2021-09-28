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

export default {
    components: {
        SearchBar,
        PokemonCard
    },

    setup() {
        const searchQuery = ref("");
        const pokemon = ref(null);


        const fetchPokemon = async () => {
            await fetch("https://pokeapi.co/api/v2/pokemon/" + searchQuery.value)
            .then(res => res.json())
            .then(data => pokemon.value = data);
        }

        onMounted(fetchPokemon);
        
        watch(searchQuery, fetchPokemon);

        return {
            pokemon,
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