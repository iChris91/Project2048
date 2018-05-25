<template>
  <div id="leaderBoard">
    <table>
      <tr>
        <td>Rank</td>
        <td>Nickname</td>
        <td>Score</td>
        <td>Time</td>
      </tr>
      <tr v-for="(score, index) in scores" v-bind:key="index" v-if="(index < 10)">
        <td>{{ index+1 }}</td>
        <td>{{ score.nickname }}</td>
        <td>{{ score.score }}</td>
        <td>{{ score.time }}</td>
      </tr>
    </table>
  </div>
</template>
<script>
import http from '@/utils/http'

export default {
  name: 'LeaderBoard',
  methods: {
    loadLeaderBoard: function () {
      http
        .get('json')
        // .get(`${this.LeaderBoard.nickname}/${this.LeaderBoard.score}/${this.LeaderBoard.time}`)
        .then(response => {
          console.log(response.data[0])
          this.scores = response.data.filter(function (score) {
            console.log('yo' + score.nickname)
            if (score.nickname !== 'name') {
              return true
            } else {
              return false
            }
          })
        })
        .catch(error => console.log(error))
    }
  },
  created () {
    this.loadLeaderBoard()
  },
  data () {
    return {
      scores: {nickname: '', score: '', time: ''}
    }
  }
}
</script>
<style>
  #leaderBoard {
    width: 1170px;
    margin: 0 auto;
    display:flex;
    justify-content: center;
  }
  #leaderBoard>table {
    width: 100%;
    margin-top:30px;
    border: 1px solid #2c3e50;
    border-collapse: collapse;
  }
  #leaderBoard>table>tr:first-of-type td {
    background: #2c3e50;
    color:white;
    border-right: 1px solid white;
  }
  #leaderBoard>table>tr>td {
    padding: 4px 0;
    border: 1px solid #2c3e50;
  }
  #leaderBoard>table>tr:nth-child(2n+2) td {
    background: whitesmoke;
  }
  #leaderBoard>table>tr:first-of-type td:last-of-type {
    border-right: none;
  }
  #leaderBoard td {
    word-break: break-all;
    overflow:hidden;
    width: 25%;
  }
</style>
