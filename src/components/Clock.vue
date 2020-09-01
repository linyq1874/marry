<template>
   <div class="date" v-html="date">
   </div>
</template>

<script>
export default {
  name: '',
  data() {
    return {
      timer: null,
      startDate: '2019-10-03 00:00:00',
      date: ''
    }
  },
  mounted() {
    this.init()
  },
  methods: {
    init() {
      this.timer = setInterval(() => {
        this.date = this.timeFn()
      }, 1000)
    },
    padZero(str) {
      return str.toString().padStart(2, '00')
    },
    timeFn() {
      //di作为一个变量传进来
      //如果时间格式是正确的，那下面这一步转化时间格式就可以不用了
      let dateBegin = new Date(this.startDate.replace(/-/g, '/')) //将-转化为/，使用new Date
      let dateEnd = new Date() //获取当前时间
      let dateDiff = dateEnd.getTime() - dateBegin.getTime() //时间差的毫秒数
      let dayDiff = this.padZero(Math.floor(dateDiff / (24 * 3600 * 1000))) //计算出相差天数
      let leave1 = dateDiff % (24 * 3600 * 1000) //计算天数后剩余的毫秒数
      let hours = this.padZero(Math.floor(leave1 / (3600 * 1000))) //计算出小时数
      //计算相差分钟数
      let leave2 = leave1 % (3600 * 1000) //计算小时数后剩余的毫秒数
      let minutes = this.padZero(Math.floor(leave2 / (60 * 1000))) //计算相差分钟数
      //计算相差秒数
      let leave3 = leave2 % (60 * 1000) //计算分钟数后剩余的毫秒数
      let seconds = this.padZero(Math.round(leave3 / 1000))
      return `<span class="day">${dayDiff}天</span> <span>${hours}</span>时 <span>${minutes}</span>分 <span class="seconds">${seconds}</span>秒`
    }
  },
  beforeDestroy() {
    clearInterval(this.timer)
  }
}
</script>

<style lang="scss">
.day {
  font-size: 8vw;
}
</style>
