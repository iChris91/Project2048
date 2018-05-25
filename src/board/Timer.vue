<template>
  <div>
    <div class="blocAside">Time :
      <!--<span id="chronoTime">00.00.00</span>-->
      <span id="chronotime">0:00:00:00</span>
      <form name="chronoForm">
        <input type="button" name="startstop" value="start!" @click="start" />
        <input type="button" name="reset" value="reset!" @click="reset" />
      </form>
    </div>
  </div>
</template>
<script>
// import chrono from './chrono.js'

export default {
  name: 'Timer',
  created () {
  },
  methods: {
    start: function () {
      // chrono.chronoStart()
      // console.log(chrono)
    },
    reset: function () {
      // chrono.chronoReset()
    }
  }
}
</script>
<style>
</style>
