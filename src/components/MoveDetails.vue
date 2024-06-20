<template>
  <span v-if="move">{{ move.accuracy }}</span>
</template>
<script setup>
import { defineProps, onBeforeMount, ref } from "vue";
import axios from "axios";

const props = defineProps({
  url: String,
});

let move = ref(null);

onBeforeMount(() => {
  console.log(props.url);
  getMoveDetails(props.url);
});

function getMoveDetails(url) {
  axios
    .get(url)
    .then((res) => {
      move.value = res.data;
    })
    .then(() => {
      console.log(move.value);
    });
}
</script>
<style scoped></style>
