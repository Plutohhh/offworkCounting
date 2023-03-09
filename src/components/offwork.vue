<template>
  <div class="offwork">
    <div>
      <span>{{ percent }}</span>
      <el-progress
        :text-inside="true"
        :stroke-width="36"
        color="#000"
        :percentage="toDecimal3(getPercent() * 100)"
      />
    </div>
    <h1>
      {{
        `距离下班还有：${offworkTime.hour}时${offworkTime.min}分${offworkTime.ss}秒${offworkTime.ms}毫秒`
      }}
    </h1>
    <el-steps direction="vertical" :active="active" :align-center="true">
      <el-step
        v-for="(item, index) in activities"
        :key="index"
        :title="item.content"
      >
        <template v-slot:description v-if="active === index">
          <span>{{ item.nowTime }}</span>
          <img v-if="item.nowTime" src="@/assets/images/gif.gif" alt="" />
        </template>
      </el-step>
    </el-steps>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue'
import dateUtil from '../utils/dateUtil'
let active = ref(0)
const activities = ref([
  {
    content: `上班\xa0\xa0\xa0${dateUtil.format(
      new Date(),
      'YYYY-MM-DD'
    )} 9:00`,
    timestamp: '',
    nowTime: '',
    color: '#0bbd87',
  },
  {
    content: `恰饭\xa0\xa0\xa0${dateUtil.format(
      new Date(),
      'YYYY-MM-DD'
    )} 12:00`,
    timestamp: '',
    nowTime: '',
    size: 'large',
  },
  {
    content: `下午上班\xa0\xa0\xa0${dateUtil.format(
      new Date(),
      'YYYY-MM-DD'
    )} 14:00`,
    timestamp: '',
    nowTime: '',
    type: 'primary',
    hollow: true,
  },
  {
    content: `下班！\xa0\xa0\xa0${dateUtil.format(
      new Date(),
      'YYYY-MM-DD'
    )} 18:00`,
    timestamp: '',
    nowTime: '',
  },
])
let offworkTime = ref('')
let percent = ref('')
onMounted(() => {
  setInterval(() => {
    offworkTime.value = getOffWorkTime()
    percent.value = `今日剩余：${Math.floor(getPercent() * 10000) / 100}%`
    setTodayTimeSteps()
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
 * 返回今日剩余工时百分比
 * @totalHour {Number} 总共工时（默认9小时）
 */
function getPercent(totalHour = 9) {
  const msLast = getMsLast()
  const totalMs = 3600000 * totalHour
  const percent = msLast / totalMs
  return percent
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
  // console.log(dateUtil.format(targeTime))
  return msLast
}

/**
 * 返回保留小数点后三位的x（补0）
 * @x {Number}
 */
function toDecimal3(x) {
  var f = parseFloat(x)
  if (isNaN(f)) {
    return false
  }
  var f = Math.round(x * 1000) / 1000
  var s = f.toString()
  var rs = s.indexOf('.')
  if (rs < 0) {
    rs = s.length
    s += '.'
  }
  while (s.length <= rs + 3) {
    s += '0'
  }
  return s
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

function setTodayTimeSteps() {
  const hour = new Date().getHours()
  if (hour < 12) {
    active.value = 0
    activities.value[active.value].nowTime = `⇦${dateUtil.format(
      new Date(),
      'HH:mm:ss'
    )}`
  } else if (hour < 14) {
    active.value = 1
    activities.value[active.value].nowTime = `⇦${dateUtil.format(
      new Date(),
      'HH:mm:ss'
    )}`
  } else if (hour < 18) {
    active.value = 2
    activities.value[active.value].nowTime = `⇦${dateUtil.format(
      new Date(),
      'HH:mm:ss'
    )}`
  } else {
    active.value = 3
    activities.value[active.value].nowTime = `⇦${dateUtil.format(
      new Date(),
      'HH:mm:ss'
    )}`
  }
}
</script>

<style scoped lang="scss">
.offwork {
  // font-size: 1rem;
  margin-left: 20px;
  margin-top: 20px;
  span {
    font-size: 26px;
    width: 15%;
    display: inline-block;
    min-width: 250px;
    vertical-align: middle;
  }
  .el-progress {
    width: 30%;
    display: inline-block;
    vertical-align: middle;
  }
  .el-steps {
    height: 300px;
    margin: 30px;
    span {
      font-size: 17px;
      margin-top: 0px;
      width: 20px;
      min-width: 83px;
      display: inline-block;
      vertical-align: middle;
    }
    img {
      display: inline-block;
      height: 60px;
      vertical-align: middle;
    }
  }
}
</style>
