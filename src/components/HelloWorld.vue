<script setup>
import { ref } from 'vue'
import subview from './subview'

defineProps({
  msg: String,
})

let str = ref('123')
function addStr() {
  str.value += '#'
}
const count = ref(0)
</script>

<template>
  <div>
    <el-button @click="addStr">add</el-button>
    <p>{{ str }}</p>
    <subview :str="str"></subview>
  </div>
</template>

<style scoped>
.read-the-docs {
  color: #888;
}
</style>
