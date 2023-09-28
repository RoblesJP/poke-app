<template>
  <search-bar v-model="searchQuery"></search-bar>

  <div class="pokemons">
    <pokemon-card
      v-if="pokemon"
      :name="pokemon.name"
      :sprite="pokemon.sprites.front_default"
      :type1="pokemon.types[0].type.name"
      :type2="pokemon.types[1]?.type.name"
      :stats="pokemon.stats"
    ></pokemon-card>
  </div>
</template>

<script setup>
import SearchBar from "@/components/SearchBar.vue";
import PokemonCard from "@/components/PokemonCard.vue";
import { ref, onBeforeMount, watch } from "vue";
import axios from "axios";

let url = "https://pokeapi.co/api/v2/pokemon/";
const searchQuery = ref("");
let pokemonNames = [];
const pokemon = ref(null);

const getPokemonNames = (url) => {
  axios.get(url).then((res) => {
    res.data.results.forEach((pokemon) => {
      pokemonNames.push(pokemon.name);
    });
    if (res.data.next != null) {
      return getPokemonNames(res.data.next);
    }
  });
};

const getPokemonByName = () => {
  let name = searchQuery.value.toLowerCase();
  if (name != null && name !== "" && pokemonNames.includes(name)) {
    axios.get(url + name).then((res) => (pokemon.value = res.data));
    console.log("request for " + name);
  }
};

onBeforeMount(() => {
  getPokemonNames(url);
});

watch(searchQuery, getPokemonByName);
</script>

<style>
.pokemons {
  display: flex;
  justify-content: center;
}
</style>
