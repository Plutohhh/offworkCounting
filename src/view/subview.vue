<template>
  <el-input v-model="str"></el-input>
</template>

<script setup>
import { defineProps, defineEmits, computed } from 'vue'
const { str } = defineProps({
  str: {
    type: String,
    default: 'xxx',
  },
})
const emit = defineEmits(['update:modelValue'])
</script>

<style scoped lang="scss"></style>
