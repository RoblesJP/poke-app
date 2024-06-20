<template>
  <article class="card pokemon_moves">
    <section class="moves-section">
      <h2>Moves</h2>
      <div class="accordion accordion-flush" id="movesAccordion">
        <move
          v-for="move in moves"
          :url="move.move.url"
          :key="move.move.name"
        ></move>
      </div>
    </section>
  </article>
</template>

<script setup>
import { defineProps, onBeforeMount } from "vue";
import Move from "@/components/Move.vue";

const props = defineProps({
  moves: Object,
});
</script>

<style scoped>
.pokemon_moves {
  overflow-y: scroll;
}
</style>
