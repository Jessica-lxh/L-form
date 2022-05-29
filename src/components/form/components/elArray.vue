<template>
  <div>
    <el-card shadow="never">
      <div v-for="(item, index) in array" :key="index">
        <div style="text-align:right">
          <el-button @click.prevent="removeChildren(index)" type="text" size="mini">删除</el-button>
        </div>
        <el-object :schema="schema" v-model="array[index]" />
      </div>
      <div style="text-align:right; margin-top:10px">
        <el-button type="primary" size="mini" icon="el-icon-plus" round plain @click="addChildren"></el-button>
      </div>
    </el-card>
  </div>
  
</template>

<script>
export default {
  name: 'el-array',
  model: {
    prop: 'array',
    event: 'change' //对应下面$emit即可
  },
  props: {
    schema: Object,
    value: [String, Array],
  },
  components: {
    elObject: () => import('../commonForm') , 
  },
  data() {
    return {
      array: [{}],
    };
  },
  watch: {
    array: {
      handler() {
        this.$emit('change', this.array)
      }
    }
  },
  methods: {
    removeChildren(index) {
        if (index !== -1) {
          this.array.splice(index, 1)
        }
      },
    addChildren() {
      this.array.push({});
    }
  },
}
</script>

<style>
.box {
  box-shadow: 0 2px 12px 0 rgba(0, 0, 0, 0.1)
}
.right {
  margin: 0 0 10px auto;
}
</style>