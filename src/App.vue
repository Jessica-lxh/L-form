<template>
  <div>
    <el-row :gutter="20">
      <el-col :span="6">
        <el-button type="primary">schema</el-button>
        <el-button type="primary" @click="changeSchema">快速增加一个输入框</el-button>
        <codemirror 
          v-model="jsonSchema"
          :options="{
            mode: 'vue',
            extraKeys: {'Ctrl-Space': 'autocomplete'},
            lineWrapping: true,
            tabSize: 2,
            matchBrackets: true
          }"></codemirror>
        <!-- <textarea v-model="jsonSchema" class="code-textarea"></textarea> -->
      </el-col>
      <el-col :span="12">
        <el-button type="primary">使用方法：{{use}}</el-button>
        <common-form :schema="schema" v-model="form" />
      </el-col>
      <el-col :span="6">
        <el-button type="primary">获取到的值：form</el-button>
        <pre>{{form}}</pre>
        <el-button size="small" type="primary" @click="change">尝试改变第二层B2的值</el-button>
      </el-col>
    </el-row>    
  </div>
</template>

<script>
import commonForm from '@/components/form/commonForm'
import { codemirror } from 'vue-codemirror-lite'
  require('codemirror/mode/javascript/javascript')
  require('codemirror/mode/vue/vue')

  require('codemirror/addon/hint/show-hint.js')
  require('codemirror/addon/hint/show-hint.css')
  require('codemirror/addon/hint/javascript-hint.js')

  require('codemirror/addon/edit/matchbrackets')


export default {
  name: 'app',
  components: {
    commonForm,
    codemirror
  },
  data() {
    return {
      use: `<common-form :schema="schema" v-model="form" />`,
      form: {}, //最终获取到的数据
      schema: {
        children: [
          {
            model: "A1",
            label: "A1 Input 输入框",
            type: "el-input",
          },
          {
            model: 'A2', 
            label: 'A2 第二层', 
            type: 'el-object', 
            children: [
              {
                model: "B1",
                label: "B1 InputNumber 计数器",
                type: "el-input-number",
              },
              {
                model: "B2",
                label: "B2 Textarea 文本框",
                type: "el-textarea",
              },
              {
                model: "B3",
                label: "B3 Upload 上传",
                type: "el-upload",
                props: {
                  mode: 'single',
                  limit: 1,
                  data: {'imageType': 2}                 
                }                  
              },
              {
                model: 'B4', 
                label: 'B4 动态增删组件', 
                type: 'el-array',  
                children: [
                  {
                    model: "C1",
                    label: "C1 Radio 单选框",
                    type: "el-radio-group",
                    options: [
                      {label: '苹果'}, 
                      {label: '西瓜'}, 
                      {label: '草莓'}
                    ]
                  },
                  /* {
                    model: "C3",
                    label: "C3 Checkbox 多选框",
                    type: "el-checkbox-group",
                    options: [
                      {label: '苹果'}, 
                      {label: '西瓜'}, 
                      {label: '草莓'}
                    ]
                  }, */
                ],
              }, 
              {
                model: 'B5', 
                label: 'B5 第三层', 
                type: 'el-object', 
                children: [
                  {
                    model: 'C2', 
                    label: 'C2 第四层', 
                    type: 'el-object', 
                    children: [
                      {
                        model: "D1",
                        label: "D1 Select 选择器",
                        type: "el-select",
                        options: [1, 2, 3]
                      },
                      /* {
                        model: "D2",
                        label: "D2 Cascader 级联选择器",
                        type: "el-cascader",
                      },   */
                      {
                        model: "D2",
                        label: "D3 第五层",
                        type: "el-object",
                        children: [
                          {
                            model: "E1",
                            label: "E1 TimePicker 时间选择器",
                            type: "el-time-select",
                          }, 
                          {
                            model: "E2",
                            label: "E2 DatePicker 日期选择器",
                            type: "el-date-picker",
                          }, 
                          /* {
                            model: "E3",
                            label: "E3 DateTimePicker 日期时间选择器",
                            type: "el-date-time-picker",
                          },  */
                          {
                            model: "E3",
                            label: "E3 第六层",
                            type: "el-object",
                            children: [
                              {
                                model: "F1",
                                label: "F1 Rate 评分",
                                type: "el-rate",
                              }, 
                              {
                                model: "F2",
                                label: "F2 ColorPicker 颜色选择器",
                                type: "el-color-picker",
                              }
                            ]
                          }, 
                        ]
                      },        
                    ]  
                  },
                  
                ]  
              },
              {
                model: 'B6', 
                label: 'B6 另一个第三层', 
                type: 'el-object', 
                children: [
                  {
                    model: "C3",
                    label: "C3 Switch 开关",
                    type: "el-switch",
                  }, 
                  {
                    model: "C4",
                    label: "C4 Slider 滑块",
                    type: "el-slider",
                  },          
                ]  
              }
            ]
          },          
        ]
      }, 
    };
  },
  computed: {
    jsonSchema:{
      get() {
        return JSON.stringify(this.schema, null, 1)
      },
      set(val) {
        this.schema = JSON.parse(val)
      }
    }
  },
  methods: {
    change() {
      this.form.A2.B2 = 'testChange'
    },
    changeSchema() {
      this.schema.children.push({
            model: "A" + Date.now(),
            label: "A" + Date.now() + " Input 输入框",
            type: "el-input",
          },)
    },
  },
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
.code-textarea {
  display: block;
  width: 100%;
  height: 100vh;
}
.CodeMirror {
  font-family: "Helvetica Neue",Helvetica,"PingFang SC","Hiragino Sans GB","Microsoft YaHei","微软雅黑",Arial,sans-serif;
  font-size: 14px;
  color: #606266;
  border: none;
  height: auto;
  width: auto;
}
</style>
