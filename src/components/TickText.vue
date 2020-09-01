<template>
   <div class="tick">
   远看山有色，近听水无声
   </div>
</template>

<script>
export default {
  name: '',
  data() {
    return {}
  },
  components: {}
}
</script>

<style lang="scss" scoped>
.tick {
  font: bold 200% Consolas, Monaco, monospace;
  border-right: 0.1em solid;
  width: 11.5em; /* fallback */
  /* width: 30ch; # of chars */
  margin: 2em 1em;
  white-space: nowrap;
  overflow: hidden;
  animation: typing 10s steps(16, end),
    /* # of steps = # of chars */ /*animation: typing 20s steps(30, end),*/
      /*英文速度*/ blink-caret 0.5s step-end infinite alternate;
}

@keyframes typing {
  from {
    width: 0;
  }
}
@keyframes blink-caret {
  50% {
    border-color: transparent;
  }
}
</style>
