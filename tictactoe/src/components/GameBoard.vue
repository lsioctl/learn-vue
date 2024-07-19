<script setup lang="ts">
import { ref, shallowReactive, shallowRef } from 'vue'
import type { Ref } from 'vue'
import SquareItem from './SquareItem.vue'

// We do not need deep reactivity as the state is only the array
// as a whole
const squareList = shallowRef(Array(9).fill(null))
const player = ref('X')

function setNextPlayer() {
  if (player.value === 'X') {
    player.value = 'O'
  } else {
    player.value = 'X'
  }
}

function onSquareClicked(index: number) {
  console.log(squareList)
  console.log(squareList.value)
  //console.log(squareList.value[0].value)
  console.log('clicked')
  console.log(index)
  // work in the immutable way => copy the state
  const nextSquareList = squareList.value.slice()

  // set the correct value
  // be wary to not do:
  // nextSquareList[index] = player
  // as it would store a Ref and not a value
  nextSquareList[index] = player.value

  console.log(nextSquareList)

  squareList.value = nextSquareList

  setNextPlayer()
}
</script>

<template>
  <div class="board">
    <div class="board_row">
      <SquareItem :player="squareList[0]" @click="() => onSquareClicked(0)" />
      <SquareItem :player="squareList[1]" @click="() => onSquareClicked(1)" />
      <SquareItem :player="squareList[2]" @click="() => onSquareClicked(2)" />
    </div>
    <div class="board_row">
      <SquareItem :player="squareList[3]" @click="() => onSquareClicked(3)" />
      <SquareItem :player="squareList[4]" @click="() => onSquareClicked(4)" />
      <SquareItem :player="squareList[5]" @click="() => onSquareClicked(5)" />
    </div>
    <div class="board_row">
      <SquareItem :player="squareList[6]" @click="() => onSquareClicked(6)" />
      <SquareItem :player="squareList[7]" @click="() => onSquareClicked(7)" />
      <SquareItem :player="squareList[8]" @click="() => onSquareClicked(8)" />
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
