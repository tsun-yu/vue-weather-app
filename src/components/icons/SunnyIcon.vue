<script setup>
defineProps({
  msg: {
    type: String,
  },
});
</script>

<template>
  <svg viewbox="-50 -50 100 100">
    <circle class="sun" cx="44" cy="44" r="22"></circle>
  </svg>
</template>

<style scoped>
svg {
  width: 100%;
  position: relative;
}
svg .sun {
  fill: #ffd633;
  stroke: rgba(255, 214, 51, 0.5);
  stroke-width: 30px;
  stroke-dasharray: 5px;
}
</style>
