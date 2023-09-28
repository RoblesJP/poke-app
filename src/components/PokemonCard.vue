<template>
  <article class="card">
    <header>
      <img :src="sprite" class="sprite" />
      <h1>{{ name }}</h1>
    </header>

    <section class="types-section">
      <h2>Type</h2>
      <div class="types-section_types section-content">
        <span>{{ type1 }}</span>
        <span v-if="type2">{{ type2 }}</span>
      </div>
    </section>

    <section class="stats-section">
      <h2>Stats</h2>
      <div class="stats-section_stats section-content">
        <stats-hexagon :stats="stats" :key="stats"></stats-hexagon>
      </div>
    </section>
  </article>
</template>

<script setup>
import StatsHexagon from "@/components/StatsHexagon.vue";
import { defineProps, onMounted, watchEffect } from "vue";

const props = defineProps({
  name: String,
  sprite: String,
  type1: String,
  type2: String,
  stats: Object,
});

onMounted(() => {
  console.log(props.stats);
});

watchEffect(props.stats);
</script>

<style scoped>
/* CARD */
.card {
  width: 300px;
  padding: 0.5rem;
  border: 1px solid black;
}

.card section {
  margin-top: 0.5rem;
}

/* SPRITE */
.sprite {
  border: 1px dashed black;
}

/* HEADER */
header {
  display: grid;
  grid-template-columns: 1fr 3fr;
  align-items: center;
}

/* SECTION */
section h2 {
  background-color: lightsalmon;
}

header h1 {
  text-transform: uppercase;
}

section .section-content {
  padding: 0.5rem;
}

/* TYPES SECTION */
.types-section span {
  text-transform: capitalize;
}

.types-section_types {
  display: flex;
}

.types-section_types span {
  flex: 1;
}

/* STATS SECTION */
.stats-section_stats {
  display: grid;
  grid-template-columns: 1fr;
  text-align: left;
  text-transform: uppercase;
  margin-top: 0.5rem;
}
</style>
