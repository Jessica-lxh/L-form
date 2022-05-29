<template>
  <el-date-picker
    v-bind:value="value"
    v-on:input="$emit('change', $event.target.value)"
    type="datetime"
    placeholder="选择日期时间">
  </el-date-picker>
</template>

<script>
export default {
  model: {
    prop: 'value',
    event: 'change'
  },
  props: {
    schema: Object,
    value: [String, Array, Object],
  }
}
</script>

<style>

</style>