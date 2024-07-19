<script setup lang="ts">

// We use Type script types instead of runtime types
defineProps<{
  player: string | null
}>()
</script>

<template>
  <div class="square">{{ player }}</div>
</template>

<style scoped>
.square {
  box-sizing: border-box;
  border: 1px solid #000;
  width: 33%;
  height: 100%;
  font-family: cursive;
  display: flex;
  justify-content: center;
  align-items: center;
}
</style>
