<template>
  <div class="container">
    <div class="timeLast">
      <h1>距離下班還有：</h1>
      <!-- <h2 class="lastTimeFont" data-content="a啊1321123">a啊1321123</h2> -->
      <h2 class="lastTimeFont" :data-content="lastTime">
        {{ lastTime }}
      </h2>
    </div>
    <div class="timePercent">
      <h1>{{ percent }}</h1>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted, computed, watch } from 'vue'
// import dateUtil from '../utils/dateUtil'
let offworkTime = ref({})
let percent = ref('')
let widthPercent = ref('')

const lastTime = computed(() => {
  return `${offworkTime.value.hour}時${offworkTime.value.min}分鐘${offworkTime.value.ss}秒${offworkTime.value.ms}毫秒`
})

watch(percent, () => {
  document.body.style.setProperty('--width', widthPercent.value)
})

onMounted(() => {
  setInterval(() => {
    offworkTime.value = getOffWorkTime()
    percent.value = `今日剩餘：${Math.floor(getPercent() * 10000) / 100}%`
    widthPercent.value = `${Math.floor(getPercent() * 10000) / 100}%`
  })
})

/**
 * 返回距离下班时间数
 */
function getOffWorkTime() {
  const msLast = getMsLast()
  const offworkTime = {}
  if (msLast < 0) {
    offworkTime.hour = Math.ceil(msLast / 3600 / 1000)
    offworkTime.min = Math.ceil((msLast / 1000 / 60) % 60)
    offworkTime.ss = Math.ceil((msLast / 1000) % 60)
    offworkTime.ms = toPatch3(msLast % 1000)
  } else {
    offworkTime.hour = Math.floor(msLast / 3600 / 1000)
    offworkTime.min = Math.floor((msLast / 1000 / 60) % 60)
    offworkTime.ss = Math.floor((msLast / 1000) % 60)
    offworkTime.ms = toPatch3(msLast % 1000)
  }
  return offworkTime
}

/**
 * 返回距离18点的毫秒数
 * @template {String} 倒计时终点（默认六点）
 */
function getMsLast(template = '2000/1/1 18:00:00') {
  let targeTime = new Date(template)
  const nowTime = new Date()
  targeTime = new Date(targeTime.setFullYear(nowTime.getFullYear()))
  targeTime = new Date(targeTime.setMonth(nowTime.getMonth()))
  targeTime = targeTime.setDate(nowTime.getDate())
  const msLast = targeTime - new Date().getTime()
  return msLast
}

/**
 * 返回三位的x（补0）
 * @x {Number}
 */
function toPatch3(x) {
  x = x.toString()
  while (x.length < 3) {
    x = '0' + x
  }
  return x
}

/**
 * 返回今日剩余工时百分比
 * @totalHour {Number} 总共工时（默认9小时）
 */
function getPercent(totalHour = 9) {
  const msLast = getMsLast()
  const totalMs = 3600000 * totalHour
  const percent = msLast / totalMs
  return percent
}
</script>

<style scoped lang="scss">
.container {
  background-color: black;
  height: 100%;
  width: 100%;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  color: #fff;
  font-weight: bolder;
  .timeLast {
    position: relative;
    text-align: left;
    margin-left: calc(100vw / 80);
    h1 {
      font-size: calc(100vw / 8);
      margin: 0;
      font-weight: bolder;
    }
    h2 {
      margin: 0;
      font-size: calc(100vw / 12);
      color: #fff;
      font-weight: bolder;
      display: inline-block;
    }

    h2:before {
      position: absolute;
      left: 0px;
      color: #ff0000;
      display: block;
      width: var(--width);
      height: calc(100vw / 8);
      content: attr(data-content); /* 伪元素的动态获取内容 */
      overflow: hidden;
      white-space: nowrap;
      font-size: calc(100vw / 12);
    }
  }
  .timePercent {
    text-align: left;
    h1 {
      margin: 0;
      font-weight: bolder;
      font-size: calc(100vw / 12);
    }
  }
}
</style>
