# lform

<p>
  <a href="https://github.com/vuejs/vue">
    <img src="https://img.shields.io/badge/vue-2.6.11-brightgreen.svg" alt="vue">
  </a>
  
  <a href="https://github.com/ElemeFE/element">
    <img src="https://img.shields.io/badge/element--ui-2.15.8-brightgreen.svg" alt="element-ui">
  </a>
  
  <a href="https://www.npmjs.com/package/form-making">
    <img src="https://img.shields.io/npm/dt/form-making" alt="downloads">
  </a>
</p>

基于Vue和Element UI实现的轻量级自定义表单搭建，支持无限嵌套表单、动态增删组件、自定义组件自动注入等，支持v-model双向绑定，是一款简单高效的表单开发工具。

[在线预览](https://jessica-lxh.github.io/L-form/)

## 使用方法
```
<template>
<common-form :schema="schema" v-model="form" />
</template>

<script>
import commonForm from '@/components/form/commonForm'

export default {
  components: {
    commonForm
  },
  data() {
    return {
      form: {}, 
      schema: {
        children: [
          {
            model: "A1",
            label: "A1 Input 输入框",
            type: "el-input",
          }
        ]
      }, 
    };
  },
}
</script>
```

## Project setup
```
npm install
```

### Compiles and hot-reloads for development
```
npm run serve
```

### Compiles and minifies for production
```
npm run build
```

### Lints and fixes files
```
npm run lint
```

