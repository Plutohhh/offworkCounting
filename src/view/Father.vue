<template>
  <div class="container">
    <h1>自定义v-model，实现父子组件间str变量的双向绑定（父子都可以编辑str）</h1>
    <span>父组件展示str：{{ str }}</span>
    <br />
    <span>父组件编辑str：</span>
    <el-button @click="clickbtn">+1</el-button>
    <br />
    <Son v-model="str"></Son>
    <br />
    <img src="@/assets/images/vmodel.png" alt="" />
    <!-- <Son
      :modelValue="str"
      @update:modelValue="newValue => (searchText = newValue)"
    /> -->
  </div>
</template>

<script setup>
import { ref } from 'vue'
import Son from '@/view/Son'
const str = ref('测试')
function clickbtn() {
  str.value += '！'
}

const discriptionFA = ref(`子组件直接v-model绑定str
<Son v-model="str"></Son>
其实v-model展开后为：
<Son :modelValue="str" @update:modelValue="updateValue" />`)
const discriptionSON = ref(`<input
    :value="modelValue"
    @input="$emit('update:modelValue', $event.target.value)"
  />
  
  `)
</script>

<style scoped lang="scss">
.container {
  height: 100%;
  width: 100%;
  padding: 0 30px 0;
  text-align: left;
  color: #3c2147;
  overflow-y: auto;
  overflow-x: hidden;
}
</style>
