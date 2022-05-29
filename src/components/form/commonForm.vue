<template>
  <form :model="tempForm">
    <el-card shadow="never">
      <el-button v-if="schema.type ==='object'" type="info" plain size="mini">{{schema.label}}</el-button>

      <div v-for="(item, index) in schema.children" :key="index">

        <span v-if="item.type != 'object'" class="form-item">{{item.label}}</span>

        <component
          v-if="!hangKey.includes(item.type)"
          :is="item.type" 
          :schema="item"
          v-model="tempForm[item.model]"
          :label="item.label"
          :placeholder="'请输入' + item.label" 
          :disabled="item.disabled"
          clearable
        />

        <!-- 尚未完成的临时组件 -->
        
        <el-radio-group 
          v-if="item.type ==='el-radio-group'"
          v-model="tempForm[item.model]"
          :disabled="item.disabled">
          <el-radio 
            v-for="(opt, index) in item.options" :key="index"
            :label="opt.label"
            :disabled="opt.disabled">{{opt.label}}</el-radio>
        </el-radio-group>

        <el-select 
          v-if="item.type ==='el-select'"
          v-model="tempForm[item.model]"
          filterable 
          :placeholder="'请选择' + item.label"
          :disabled="item.disabled"
          :multiple="item.multiple"
          clearable
          style="width: 100% !important">
          <el-option
            v-for="(opt, index) in item.options" :key="index"
            :label="opt"
            :value="index + 1"
            :disabled="opt.disabled"></el-option>
        </el-select>

        <el-upload
          class="avatar-uploader"
          :show-file-list="false"
          action="#"
          :auto-upload="false"
          accept="image/*"
          :file-list="fileList"
          v-if="item.type === 'el-upload' "
          :on-change="function(file){return handleUploadChange(file, item.model)}">
          <img v-if="tempForm[item.model]" :src="imageUrl[item.model]" class="avatar">
          <i v-else slot="default" class="el-icon-plus avatar-uploader-icon"></i>
        </el-upload>
      </div>
    </el-card>    
  </form>    
</template>

<script>

  /* 
  * 导入/form/components中的自定义组件 
  */
  const requireComponent = require.context('./components/', false, /\.vue$/)

  const cmps = {}

  requireComponent.keys().forEach(fileName => {
    const reqCom = requireComponent(fileName)
    const reqComName = fileName.split('/')[fileName.split('/').length - 1].split('.')[0]
    cmps[reqComName] = reqCom.default || reqCom;
  })

  /* 尚未施工完成的组件 */
  const hang = ['el-radio-group', 'el-checkbox-group', 'el-select', 'el-upload']

  export default {
    name: "el-object",
    model: {
      prop: 'tempForm',
      //对应下面$emit
      event: 'change' 
    },
    props: {
      //表单信息
      schema: Object, 
      //表单数据
      form: Object,
    },
    components: {
      ...cmps
    },
    data() {
      return {
        tempForm: {},
        //图片数据
        imageUrl: {},
        fileList: [],
        //尚未完成的组件key值
        hangKey: hang
      }
    },
    watch: {
      tempForm: {
        handler() {
          this.$emit('change', this.tempForm)
        }
      }
    },
    methods: {
      handleUploadChange(file, model) {
        console.log(file, model)
        //将图片链接赋值给image的响应属性，实现图片预览
        this.imageUrl[model] = URL.createObjectURL(file.raw)
        //用 this.$set 实现对象响应属性
        this.$set( this.tempForm, model, this.imageUrl )
      }
    }
  }
</script>

<style>
  body {
    font-family: "Helvetica Neue",Helvetica,"PingFang SC","Hiragino Sans GB","Microsoft YaHei","微软雅黑",Arial,sans-serif;
    font-size: 14px;
    color: #606266
  }
  .form-item {
    line-height: 40px;
    padding: 0 12px 0 0;
  }

  .avatar-uploader .el-upload {
    border: 1px dashed #d9d9d9;
    border-radius: 6px;
    cursor: pointer;
    position: relative;
    overflow: hidden;
  }
  .avatar-uploader .el-upload:hover {
    border-color: #409EFF;
  }
  .avatar-uploader-icon {
    font-size: 28px;
    color: #8c939d;
    width: 178px;
    height: 178px;
    line-height: 178px !important;
    text-align: center;
  }
  .avatar {
    width: 178px;
    height: 178px;
    display: block;
  }
</style>
