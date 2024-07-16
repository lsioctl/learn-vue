<script setup lang="ts">
import { ref } from 'vue'
import type { Ref } from 'vue'
import SquareItem from './SquareItem.vue'
</script>

<template>
  <div class="board">
    <div class="board_row">
      <SquareItem />
      <SquareItem />
      <SquareItem />
    </div>
    <div class="board_row">
      <SquareItem />
      <SquareItem />
      <SquareItem />
    </div>
    <div class="board_row">
      <SquareItem />
      <SquareItem />
      <SquareItem />
    </div>
  </div>
</template>

<style scoped>
.board {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 50%;
  aspect-ratio: 1/1;
  flex-direction: column;
}

.board_row {
  height: 33%;
  width: 100%;
  display: flex;
  flex-direction: row;
}
</style>
