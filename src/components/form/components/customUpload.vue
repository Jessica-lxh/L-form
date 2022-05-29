<template>
  <div>
    <el-upload
      action="#"
      :headers="{'token': token}"
      :data="schema.props.data"
      :name="'multipartFile'"
      :file-list="fileList"
      :limit="schema.props.limit"
      multiple
      list-type="picture-card"
      :on-preview="handlePictureCardPreview"
      :on-remove="handleRemove"
      :on-success="handleSuccess"
      :on-exceed="handleExceed">
      <i class="el-icon-plus"></i>
    </el-upload>
    <!-- <el-dialog :visible.sync="dialogVisible">
      <img width="100%" :src="dialogImageUrl" alt="">
    </el-dialog> -->
    

  </div>
</template>

<script>

export default {
  props: {
    schema: Object,
    value: [String, Array],
  },
  data() {
    return {
      token: sessionStorage.getItem('token'),

      //fileList: '',

      dialogImageUrl: '',
      dialogVisible: false,

    }
  },
  computed: {
    fileList: function () {
      let list = []
      if (this.value) {
        this.value.forEach((item) => {
          //console.log(item)
          list.push({
            name: item.imageName,
            url: this.baseURL + item.imageAddr
          })
        })
      }
      return list
    }
  },
  methods: {
    handleRemove(file, fileList) {
      console.log(file, fileList);
    },
    handlePictureCardPreview(file) {
      this.dialogImageUrl = file.url;
      this.dialogVisible = true;
    },
    handleSuccess(r, f, fileList) {
      console.log(r, f, fileList)
      this.$emit('onChange', fileList)
      /* console.log(2, fileList, path, model)
      let url = path.slice()
      fileList.forEach((item, index) => {
        this._set(this.tempForm, [url, index, model], item.response.annexId)
      })
      console.log(this.form) */
      //this.handleFormChange()
    },
    /* handleChange(fileList, path, model) {
      console.log(1, fileList, path, model)
    }, */
    handleExceed() {
      this.$message.error('图片张数超出限制')
    }
  },
}
</script>

<style>

</style>