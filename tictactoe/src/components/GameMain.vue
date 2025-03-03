<script setup lang="ts">

import { ref, shallowRef } from 'vue';
import type { ShallowRef } from 'vue';
import GameBoard from './GameBoard.vue';

// We do not need deep reactivity as the state is only the array
// as a whole
// this would have worked but really is overkill
// const squareList = ref(Array(9).fill(null))
const squareList: ShallowRef<null[]|string[]> = shallowRef(Array(9).fill(null));

const player = ref('X');
const winner = ref('None');

function setNextPlayer() {
  if (player.value === 'X') {
    player.value = 'O';
  } else {
    player.value = 'X';
  }
}

function getWinningIndexes() {
  // Still have to figure a proper algorithm
  // in the meantime, checking against all the solutions should be fast enough ?
  const winning_indexes = [];

  // column indexes
  winning_indexes.push([0, 3, 6]);
  winning_indexes.push([1, 4, 7]);
  winning_indexes.push([2, 5, 8]);

  // row indexes
  winning_indexes.push([0, 1, 2]);
  winning_indexes.push([3, 4, 5]);
  winning_indexes.push([6, 7, 8]);

  // diagonal indexes
  winning_indexes.push([0, 4, 8]);
  winning_indexes.push([2, 4, 6]);

  return winning_indexes;
}

const WINNING_INDEXES = getWinningIndexes();

function onSquareClicked(index: number) {
  console.log('clicked');
  console.log(index);
  
  if (winner.value === 'None') {
    // only change if the current square is not yet clicked
    if (squareList.value[index] === null) {
      // work in the immutable way => copy the state
      const nextSquareList = squareList.value.slice();

      // set the correct value
      // be wary to not do:
      // nextSquareList[index] = player
      // as it would store a Ref and not a value
      nextSquareList[index] = player.value;

      // First ensure history contains no future
      // move, as we are creating a new future by clicking
      //const nextHistory = history.slice(0, historyIndex);
      // const nextHistory = history.slice();
      // nextHistory.push(nextSquares);

      // TODO: is a race condition possible here ? => should update both in
      // the same operation
      // update the history
      // setHistory(nextHistory);
      // setHistoryIndex(historyIndex + 1);

      // set the new state
      squareList.value = nextSquareList;

      const computedWinner = checkWinner(nextSquareList);

      if (computedWinner !== 'None') {
          winner.value = computedWinner;
          console.log('wiiiin');
      }

      setNextPlayer();
    }
  }
}

function checkWinner(squareList: null[] | string[]) {
  let winner = 'None';

  // some() stops on the first true return
  WINNING_INDEXES.some(index_list => {
    // test against the index_list

    // first identify the player
    const player = squareList[index_list[0]];

    // only parse if the square is marked by a player
    if (player !== null) {
      // every() stops on the first false return
      const result = index_list.every(idx => {
        return squareList[idx] === player;
      });

      // feels clumsy to modify in a some callback
      // Fonctional Programming paradigms loves more immutable things
      if (result !== false) {
        winner = player;
      }

      return result;
    // no player, return false and go to the next some() iteration
    } else {
        return false;
    }
  });

  return winner;
}


</script>

<template>
    <GameBoard :squareList="squareList" :squareClickedCb="onSquareClicked"/>
</template>