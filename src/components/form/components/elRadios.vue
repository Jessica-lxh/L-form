<template>
  <el-radio-group 
    :value="value"
    @change="$emit('change', value)">
    <el-radio 
      v-for="(opt, index) in schema.options" :key="index"
      :label="opt.label"
      :disabled="opt.disabled">{{opt.label}}</el-radio>
  </el-radio-group>
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