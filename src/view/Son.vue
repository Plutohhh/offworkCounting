<template>
  <span>子组件：</span>
  <input
    :value="modelValue"
    @input="$emit('update:modelValue', $event.target.value)"
  />
  <!-- <input v-model="modelValue" /> -->
</template>

<script setup>
const { modelValue } = defineProps({
  modelValue: {
    type: String,
    default: '',
  },
})
// const emit = defineEmits(['update:modelValue'])
</script>

<style scoped lang="scss">
input {
  width: 250px;
}
</style>
