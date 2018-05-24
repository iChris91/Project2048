<template>
  <div id="board">
    <h1>2048 Project</h1>
    <table>
      <tr class="line" v-for="boardLine in boardGame">
        <td class="tile" v-for="boardTile in boardLine">
          <span v-if="boardTile !== 0">{{ boardTile }}</span>
        </td>
      </tr>
    </table>
  </div>
</template>
<script>
import board from '@/board/board.js'

export default {
  name: 'Home',
  created () {
    board.init(4)
    console.log(board.squares)
    this.boardGame = board.squares
    console.log(this.boardGame)
  },
  data () {
    return {
      boardGame: []
    }
  }
}
</script>
<style>
  #board {
    width: 1170px;
    margin: 0 auto;
  }
  #board>table {
    width:600px;
    margin:0 auto;
    background: lightslategrey;
    padding: 10px;
  }
  .tile {
    border:1px solid grey;
    width: 148px;
    height:148px;
    margin: 1px;
    background: whitesmoke;
    font-size:50px;
  }
</style>
