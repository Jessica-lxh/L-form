<template>
  <textarea
    v-bind:value="value"
    v-on:input="$emit('change', $event.target.value)"
    :placeholder="'请输入' + schema.label" 
    class="form-textarea"
    clearable
  />
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
body {
  font-family: "Helvetica Neue",Helvetica,"PingFang SC","Hiragino Sans GB","Microsoft YaHei","微软雅黑",Arial,sans-serif;
  font-size: 14px;
  color: #606266
}
.form-textarea {
  display: block;
  resize: vertical;
  padding: 5px 15px;
  line-height: 1.5;
  box-sizing: border-box;
  width: 100%;
  font-size: inherit;
  color: #606266;
  background-color: #FFFFFF;
  background-image: none;
  border: 1px solid #DCDFE6;
  border-radius: 4px;
  transition: border-color 0.2s;
  outline: 1px ;
}
textarea::-webkit-input-placeholder { 
  color: #C0C4CC;
}  
textarea:-moz-placeholder { 
  color: #C0C4CC;
} 
textarea::-moz-placeholder { 
  color: #C0C4CC;
} 
textarea:-ms-input-placeholder { 
  color: #C0C4CC;
}
</style>