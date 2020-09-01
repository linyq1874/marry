<template>
  <div class="FlipClock">
    <Flipper ref="flipperHour1" />
    <Flipper ref="flipperHour2" />
    <em>:</em>
    <Flipper ref="flipperMinute1" />
    <Flipper ref="flipperMinute2" />
    <em>:</em>
    <Flipper ref="flipperSecond1" />
    <Flipper ref="flipperSecond2" />
  </div>
</template>

<script>
import Flipper from './Flipper'
export default {
  name: 'FlipClock',
  data() {
    return {
      timer: null,
      d1: '2019-10-03 00:00:00',
      flipObjs: [],
    }
  },
  components: {
    Flipper,
  },
  methods: {
    // 初始化数字
    init() {
      let now = new Date()
      let nowTimeStr = this.formatDate(new Date(now.getTime()), 'hhiiss')
      for (let i = 0; i < this.flipObjs.length; i++) {
        this.flipObjs[i].setFront(nowTimeStr[i])
      }
    },
    // 开始计时
    run() {
      this.timer = setInterval(() => {
        // 获取当前时间
        let now = new Date()
        let nowTimeStr = this.formatDate(new Date(now.getTime() - 1000), 'hhiiss')
        let nextTimeStr = this.formatDate(now, 'hhiiss')
        for (let i = 0; i < this.flipObjs.length; i++) {
          if (nowTimeStr[i] === nextTimeStr[i]) {
            continue
          }
          console.log('nowTimeStr[i], nextTimeStr[i]', nowTimeStr[i], nextTimeStr[i]);

          this.flipObjs[i].flipDown(nowTimeStr[i], nextTimeStr[i])
        }
        // this.timeFn()
      }, 1000)
    },
    // 正则格式化日期
    formatDate(date, dateFormat) {
      /* 单独格式化年份，根据y的字符数量输出年份
     * 例如：yyyy => 2019
            yy => 19
            y => 9
     */
      if (/(y+)/.test(dateFormat)) {
        dateFormat = dateFormat.replace(RegExp.$1, (date.getFullYear() + '').substr(4 - RegExp.$1.length))
      }
      // 格式化月、日、时、分、秒
      let o = {
        'm+': date.getMonth() + 1,
        'd+': date.getDate(),
        'h+': date.getHours(),
        'i+': date.getMinutes(),
        's+': date.getSeconds(),
      }
      for (let k in o) {
        if (new RegExp(`(${k})`).test(dateFormat)) {
          // 取出对应的值
          let str = o[k] + ''
          /* 根据设置的格式，输出对应的字符
           * 例如: 早上8时，hh => 08，h => 8
           * 但是，当数字>=10时，无论格式为一位还是多位，不做截取，这是与年份格式化不一致的地方
           * 例如: 下午15时，hh => 15, h => 15
           */
          dateFormat = dateFormat.replace(RegExp.$1, RegExp.$1.length === 1 ? str : this.padLeftZero(str))
        }
      }
      return dateFormat
    },
    // 日期时间补零
    padLeftZero(str) {
      return ('00' + str).substr(str.length)
    },
    timeFn() {
      //di作为一个变量传进来
      //如果时间格式是正确的，那下面这一步转化时间格式就可以不用了
      var dateBegin = new Date(this.d1.replace(/-/g, '/')) //将-转化为/，使用new Date
      var dateEnd = new Date() //获取当前时间
      var dateDiff = dateEnd.getTime() - dateBegin.getTime() //时间差的毫秒数
      var dayDiff = Math.floor(dateDiff / (24 * 3600 * 1000)) //计算出相差天数
      var leave1 = dateDiff % (24 * 3600 * 1000) //计算天数后剩余的毫秒数
      var hours = Math.floor(leave1 / (3600 * 1000)) //计算出小时数
      //计算相差分钟数
      var leave2 = leave1 % (3600 * 1000) //计算小时数后剩余的毫秒数
      var minutes = Math.floor(leave2 / (60 * 1000)) //计算相差分钟数
      //计算相差秒数
      var leave3 = leave2 % (60 * 1000) //计算分钟数后剩余的毫秒数
      var seconds = Math.round(leave3 / 1000)
      console.log(' 相差 ' + dayDiff + '天 ' + hours + '小时 ' + minutes + ' 分钟' + seconds + ' 秒')
    },
  },
  mounted() {
    this.flipObjs = [this.$refs.flipperHour1, this.$refs.flipperHour2, this.$refs.flipperMinute1, this.$refs.flipperMinute2, this.$refs.flipperSecond1, this.$refs.flipperSecond2]
    this.init()
    this.run()
  },
}
</script>

<style>
.FlipClock {
  text-align: center;
}
.FlipClock .M-Flipper {
  margin: 0 0.3vw;
}
.FlipClock em {
  display: inline-block;
  line-height: 10.2vw;
  font-size: 6.6vw;
  font-style: normal;
  vertical-align: top;
}
</style>
