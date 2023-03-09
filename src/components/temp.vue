<template>
  <h2 class="hf" :data-content="temp.value">{{ temp.value }}</h2>
  <span class="hf" data-content="e">e</span>
  <span class="hf" data-content="b">b</span>
  <span class="hf" data-content="前">前</span>
  <span class="hf" data-content="端">端</span>
</template>

<script setup>
import { defineProps, defineEmits, computed, ref } from 'vue'
const word = ref('acbf')
const temp = computed(() => {
  return word
})
</script>

<style scoped lang="scss">
.hf {
  display: inline-block;
  font-size: 80px;
  line-height: 80px;
  color: #000;
  position: relative;
  overflow: hidden;
  white-space: pre; /* 处理空格 */
}
.hf:before {
  position: absolute;
  left: 0;
  top: 0;
  color: #f00;
  display: block;
  width: 30%; /*如果想变色一半文字，就设置50%*/
  content: attr(data-content); /* 伪元素的动态获取内容 */
  overflow: hidden;
}
</style>
