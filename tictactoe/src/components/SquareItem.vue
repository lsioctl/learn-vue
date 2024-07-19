<script setup lang="ts">
import { ref } from 'vue'
import type { Ref } from 'vue'

defineProps({
  player: String
})
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
