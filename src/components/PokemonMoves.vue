<template>
  <article class="card pokemon_moves">
    <section class="moves-section">
      <h2>Moves</h2>
      <div class="accordion accordion-flush" id="movesAccordion">
        <move-item
          v-for="move in moves"
          :url="move.move.url"
          :key="move.move.name"
        ></move-item>
      </div>
    </section>
  </article>
</template>

<script setup>
import { defineProps } from "vue";
import MoveItem from "@/components/MoveItem.vue";

defineProps({
  moves: Object,
});
</script>

<style scoped>
.pokemon_moves {
  overflow-y: scroll;
}
</style>
