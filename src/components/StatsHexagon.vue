<template>
  <canvas id="canvas"></canvas>
</template>

<script setup>
import { defineProps, onMounted } from "vue";

const props = defineProps({
  stats: Object,
});

let ctx;
const a = (2 * Math.PI) / 6;
const r = 120;
let letterMMeasurements;
const maxStatValue = 255;

onMounted(() => {
  const canvas = document.getElementById("canvas");
  ctx = canvas.getContext("2d");

  letterMMeasurements = ctx.measureText("M");

  // Get the DPR and size of the canvas
  const dpr = window.devicePixelRatio;
  const rect = canvas.getBoundingClientRect();

  // Set the "actual" size of the canvas
  canvas.width = rect.width * dpr;
  canvas.height = rect.height * dpr;

  // Scale the context to ensure correct drawing operations
  ctx.scale(dpr, dpr);

  // Set the "drawn" size of the canvas
  canvas.style.width = `${rect.width}px`;
  canvas.style.height = `${rect.height}px`;

  ctx.textAlign = "center";
  ctx.font = "12px Lato";
  ctx.textBaseline = "middle";

  drawOuterHexagon(canvas.width / 2, canvas.height / 2);
  drawStatsHexagon(canvas.width / 2, canvas.height / 2);
  drawOuterHexagonLines(canvas.width / 2, canvas.height / 2);
});

function drawOuterHexagon(x, y) {
  ctx.beginPath();

  Object.entries(props.stats).forEach(([, value], index) => {
    ctx.lineTo(x + r * Math.cos(a * index), y + r * Math.sin(a * index));

    drawStatTitles(
      x +
        (r + ctx.measureText(value.stat.name.split("-")[0]).width / 2 + 10) *
          Math.cos(a * index),
      y +
        (r + letterMMeasurements.width * value.stat.name.split("-").length) *
          Math.sin(a * index),
      value.stat.name
    );
  });

  ctx.closePath();
  ctx.stroke();
}

function drawStatTitles(x, y, statName) {
  const words = statName.split("-");

  words.forEach((word, index) => {
    ctx.fillText(word.toUpperCase(), x, y + index * letterMMeasurements.width);
  });
}

function drawOuterHexagonLines(x, y) {
  ctx.lineWidth = 0.1;
  Object.entries(props.stats).forEach(([,], index) => {
    ctx.beginPath();
    ctx.moveTo(x, y);
    ctx.lineTo(x + r * Math.cos(a * index), y + r * Math.sin(a * index));
    ctx.closePath();
    ctx.strokeStyle = "gray";
    ctx.stroke();
  });
}

function drawStatsHexagon(x, y) {
  console.log(x);
  console.log(y);
  ctx.beginPath();

  Object.entries(props.stats).forEach(([, value], index) => {
    ctx.lineTo(
      x + (value.base_stat / maxStatValue) * r * Math.cos(a * index),
      y + (value.base_stat / maxStatValue) * r * Math.sin(a * index)
    );
  });

  ctx.closePath();
  ctx.fillStyle = "lightsalmon";
  ctx.fill();
  ctx.stroke();
}
</script>

<style scoped>
#canvas {
  width: 100%;
  aspect-ratio: 16 / 9;
}
</style>
