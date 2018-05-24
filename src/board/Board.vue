<template>
  <div id="board"></div>
</template>
<script>
import board from '@/board/board.js'

export default {
  name: 'Board',
  created () {
    board.init(4)
  }
}
</script>
<style></style>
