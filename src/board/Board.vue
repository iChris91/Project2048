<template>
  <div>
    <div id="board">
      <div id="over" v-if="over">
        <p>You lost with <br /><strong>{{ BoardPoints }}</strong><br />points</p>
        <button @click="closeOver">Ok</button>
      </div>
      <div id="boardGame">
        <div class="tile" v-bind:key="index" v-for="(line, index) in boardGame">
          <div class="cell" v-bind:key="index" v-for="(tile, index) in line" :class="'c'+tile">
            <span v-if="tile !== 0">{{ tile }}</span>
          </div>
        </div>
      </div>
      <div id="buttons">
        <h3>Controls</h3>
        <button @click="buttonClick(37)">Left</button>
        <button @click="buttonClick(39)">Right</button>
        <button @click="buttonClick(38)">Up</button>
        <button @click="buttonClick(40)">Down</button>
        <br />
        <div class="blocAside">Score : {{ BoardPoints }}</div>
        <timer></timer>
        <button @click="start">Start</button>
        <button @click="reset">Reset</button>
        <br />
        <p>You can use your keyboard too !</p>
      </div>
    </div>
    <leader-board></leader-board>
  </div>
</template>
<script>
import board from '@/board/board.js'
import LeaderBoard from './LeaderBoard.vue'
import Timer from './Timer.vue'

export default {
  name: 'Board',
  components: { LeaderBoard, Timer },
  methods: {
    closeOver: function () {
      this.over = false
    },
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
      this.BoardPoints = board.points
      this.over = board.over
      this.$forceUpdate()
    },
    buttonClick: function (param) {
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
      this.BoardPoints = board.points
      this.over = board.over
      this.$forceUpdate()
    },
    start: function () {
      console.log('start')
    },
    reset: function () {
      board.init(4)
      this.boardGame = board.squares
    }
  },
  created () {
    board.init(4)
    console.log(board.squares)

    this.boardGame = board.squares
    console.log(this.boardGame)
    console.log(window.addEventListener('keydown', this.catchKeys))
    this.over = board.over
  },
  data () {
    return {
      boardGame: [],
      BoardPoints: '',
      over: ''
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
  #board>div#boardGame {
    background: #2c3e50;
    padding: 10px;
    display: flex;
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
    background: #2c3e50;
    color:white;
    font-weight: normal;
    letter-spacing: 2px;
  }
  .tile {
    display: flex;
    flex-direction: column;
  }
  .blocAside {
    border : 1px solid #2c3e50;
    margin-left: 15px;
    padding: 15px;
    margin-top:15px;
  }
  .blocAside:last-of-type {
    margin-bottom: 15px;
  }
  .cell {
    border:1px solid grey;
    border-radius: 2px;
    width: 148px;
    height:148px;
    margin: 1px;
    background: whitesmoke;
    font-size:50px;
  }
  .cell.c8>span {
    background: lightslategray;
  }
  .cell.c16>span {
    background: lightseagreen;
  }
  .cell.c32>span {
    background: lightpink;
  }
  .cell.c64>span {
    background: lightcoral;
  }
  .cell.c128>span {
    background: lightsteelblue;
  }
  .cell.c256>span {
    background: lightcoral;
  }
  .cell.c512>span {
    background: lightgoldenrodyellow;
  }
  .cell>span {
    display: inline-block;
    line-height: 148px;
    width: 100%;
    height:100%;
    background-color: lightcyan;
  }
  #over {
    text-transform: uppercase;
    position: fixed;
    left: 5%;
    right:5%;
    top: 5%;
    bottom:5%;
    width: 90%;
    height:auto;
    color: whitesmoke;
    background: rgba(44, 62, 80, 0.9);
    border : 1px solid #2c3e50;
    font-size:400%;
    padding-top:50px;
  }
  #over strong {
    display: inline-block;
    padding:15px;
    font-size:300%;
    color: red;
    padding: 0 50px;
    margin: 30px auto;
    border : 5px solid red;
  }
  #over p {
    margin-bottom:0;
  }
  #over button {
    padding:15px 50px;
  }
</style>
