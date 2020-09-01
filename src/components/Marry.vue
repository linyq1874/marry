<template>
  <div class="marry">
    <figure class="hearts">
      <section class="heart" v-for="(_, index) in 5" :key="index">
        <div class="plane plane-left">
          <div class="half-heart"></div>
        </div>
        <div class="plane plane-right">
          <div class="half-heart"></div>
        </div>
      </section>
    </figure>
    <div class="together">
      <flip-clock />
    </div>
  </div>
</template>

<script>
import FlipClock from '../common/FlipClock'
export default {
  name: '',
  data() {
    return {}
  },
  components: {
    FlipClock
  },
}
</script>

<style lang="scss" scoped>
$red: palevioletred;

.marry {
  margin: 0;
  height: 100vh;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  background-color: #f3f3f3;
  overflow: hidden;

  .hearts {
    width: 100vw;
    height: 20vw;
    box-sizing: border-box;
    padding: 0 5vw;
    display: flex;
    align-items: center;
    justify-content: space-between;
    .heart {
      width: 15vw;
      height: 15vw;
      position: relative;
      display: flex;
      align-items: center;
      justify-content: center;
      animation: rotate 5s ease-in-out infinite;
      transform-style: preserve-3d;
      .plane {
        position: absolute;
        opacity: 0.8;
      }
      .plane-right {
        transform: rotateY(90deg); /* 因为此处为 90 度垂直, 所以并不可见 */
      }
      .half-heart {
        width: 7.5vw;
        height: 7.5vw;
        background-color: pink;
        transform: rotate(-45deg);
      }
      .half-heart:before,
      .half-heart:after {
        content: '';
        width: 7.5vw;
        height: 7.5vw;
        background-color: pink;
        border-radius: 100%;
        position: absolute;
      }
      .half-heart:before {
        top: -3.25vw;
        left: 0;
      }
      .half-heart:after {
        top: 0;
        left: 3.25vw;
      }
    }
    .heart:nth-of-type(1) {
      animation-delay: -5s;
    }
    .heart:nth-of-type(2) {
      animation-delay: -4s;
    }
    .heart:nth-of-type(3) {
      animation-delay: -3s;
    }
    .heart:nth-of-type(4) {
      animation-delay: -2s;
    }
    .heart:nth-of-type(5) {
      animation-delay: -1s;
    }
  }

  /* keyframes */
  @keyframes rotate {
    0% {
      transform: rotateY(0deg) rotateZ(25deg) translateY(7.5vw);
    }
    50% {
      transform: rotateY(270deg) rotateZ(25deg) translateY(-7.5vw);
    }
    100% {
      transform: rotateY(360deg) rotateZ(25deg) translateY(7.5vw);
    }
  }

  .together {
    width: 100vw;
    height: 20vh;
    border-bottom: 1px solid;
  }
}
</style>
