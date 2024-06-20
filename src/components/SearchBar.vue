<template>
  <form id="search">
    <input
      placeholder="Pokemon name..."
      :value="modelValue"
      @input="$emit('update:modelValue', $event.target.value)"
    />
  </form>
</template>

<script setup>
import { defineProps } from "vue";

const props = defineProps({
  modelValue: String,
});
</script>

<style scoped>
form {
  margin-block: 2rem;
}

input {
  width: 100%;
  max-width: 500px;
  padding: 0.5rem;
  font-size: 1.4rem;
}
</style>
