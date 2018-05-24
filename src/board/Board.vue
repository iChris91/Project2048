<template>
  <div id="board">
    <table>
      <tr class="line" v-for="line in boardGame">
        <td class="tile" v-for="tile in line">
          <span v-if="tile !== 0">{{ tile }}</span>
        </td>
      </tr>
    </table>
    <div id="buttons">
      <h3>Controls</h3>
      <button>Left</button>
      <button>Right</button>
      <button>Up</button>
      <button>Down</button>
      <br />
      <button>Start</button>
      <button>Reset</button>
    </div>
  </div>
</template>
<script>
import board from '@/board/board.js'

export default {
  name: 'Board',
  methods: {
    catchKeys: function (event) {
      console.log(event)
      var param = event.keyCode
      switch (param) {
        case 37:
          console.log('case ' + param)
          board.move('left')
          break
        case 38:
          console.log('case ' + param)
          board.move('up')
          break
        case 39:
          console.log('case ' + param)
          board.move('right')
          break
        case 40:
          console.log('case ' + param)
          board.move('down')
          break
      }
      this.$forceUpdate()
    }
  },
  created () {
    board.init(4)
    console.log(board.squares)

    this.boardGame = board.squares
    console.log(this.boardGame)
    console.log(window.addEventListener('keydown', this.catchKeys))
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
    display:flex;
    justify-content: center;
  }
  #board>table {
    width:600px;
    background: lightslategrey;
    padding: 10px;
  }
  #buttons {
    display: flex;
    flex-direction: column;
  }
  #buttons>button {
    width: 300px;
    padding: 10px;
    margin-bottom:15px;
    margin-left: 15px;
  }
  #buttons h3 {
    font-size:150%;
    border: 1px solid grey;
    margin-left: 15px;
    padding: 15px;
    margin-top:0;
    background: lightslategrey;
    color:white;
    font-weight: normal;
    letter-spacing: 2px;
  }
  .tile {
    border:1px solid grey;
    border-radius: 2px;
    width: 148px;
    height:148px;
    margin: 1px;
    background: whitesmoke;
    font-size:50px;
  }
  .tile>span {
    display: inline-block;
    line-height: 148px;
    width: 100%;
    height:100%;
    background-color: lightcyan;
  }
</style>
