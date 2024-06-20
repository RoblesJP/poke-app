<template>
  <div class="accordion-item" v-if="move">
    <h2 class="accordion-header">
      <button
        class="accordion-button collapsed"
        type="button"
        data-bs-toggle="collapse"
        :data-bs-target="'#' + move.name.split('-').join('')"
        aria-expanded="false"
        :aria-controls="move.name.split('-').join('')"
      >
        {{ move.name.split("-").join(" ").toUpperCase() }}
        <span :class="'badge ' + 'move-type_' + move.type.name">{{
          move.type.name
        }}</span>
        <span
          :class="'badge border ' + 'damage-class_' + move.damage_class.name"
          >{{ move.damage_class.name }}</span
        >
      </button>
    </h2>
    <div
      :id="move.name.split('-').join('')"
      class="accordion-collapse collapse"
      data-bs-parent="#movesAccordion"
    >
      <div class="accordion-body"></div>
    </div>
  </div>
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

<style scoped>
.badge {
  margin-left: 0.5rem;
}

.move-type_electric {
  background-color: #f8ba24;
}

.move-type_normal {
  background-color: #989a98;
}

.move-type_water {
  background-color: #2979ea;
}

.move-type_fighting {
  background-color: #fd761e;
}

.move-type_ground {
  background-color: #88481f;
}

.move-type_poison {
  background-color: #893ac4;
}

.move-type_psychic {
  background-color: #eb3771;
}

.move-type_dark {
  background-color: #473937;
}

.move-type_ghost {
  background-color: #673966;
}

.move-type_fairy {
  background-color: #ec68eb;
}

.move-type_rock {
  background-color: #a8a27a;
}

.move-type_steel {
  background-color: #599ab1;
}

.move-type_grass {
  background-color: #3a9a29;
}

.move-type_bug {
  background-color: #899921;
}

.move-type_flying {
  background-color: #7bb4ec;
}

.move-type_ice {
  background-color: #3fd5fd;
}

.move-type_dragon {
  background-color: #4959db;
}

.move-type_fire {
  background-color: #e11e28;
}

.damage-class_physical {
  color: #e96666;
}

.damage-class_special {
  color: #4571f1;
}

.damage-class_status {
  color: #959595;
}
</style>
