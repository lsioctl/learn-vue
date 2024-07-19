<script setup lang="ts">

import SquareItem from './SquareItem.vue';

defineProps<{
  squareList: null[] | string[]
  squareClickedCb: (index: number) => void
}>()


</script>

<template>
  <div class="board">
    <div class="board_row">
      <SquareItem :player="squareList[0]" @click="() => squareClickedCb(0)" />
      <SquareItem :player="squareList[1]" @click="() => squareClickedCb(1)" />
      <SquareItem :player="squareList[2]" @click="() => squareClickedCb(2)" />
    </div>
    <div class="board_row">
      <SquareItem :player="squareList[3]" @click="() => squareClickedCb(3)" />
      <SquareItem :player="squareList[4]" @click="() => squareClickedCb(4)" />
      <SquareItem :player="squareList[5]" @click="() => squareClickedCb(5)" />
    </div>
    <div class="board_row">
      <SquareItem :player="squareList[6]" @click="() => squareClickedCb(6)" />
      <SquareItem :player="squareList[7]" @click="() => squareClickedCb(7)" />
      <SquareItem :player="squareList[8]" @click="() => squareClickedCb(8)" />
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
