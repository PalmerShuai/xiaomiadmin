<template>
<el-form ref="form" :model="form" label-width="80px">
  <el-form-item label="种类名称">
    <el-input v-model="form.goodsname"></el-input>
  </el-form-item>

   <el-form-item>
    <el-button type="primary" @click="onSubmit">立即创建</el-button>
    <el-button>取消</el-button>
  </el-form-item>
  </el-form>
</template>

<script>
import axios from 'axios'

export default {
  name: 'CreateUser',
  components: {  },
   data() {
      return {
        form: {
          goodsname: '',

        }
      }
    },
     methods: {
      onSubmit() {
        axios.post('/goodskind',{
         goodskindname: this.form.goodsname,

        }).then(res=>{
          if(res.data.code=20000){
            this.$message({
          message: res.data.msg,
          type: 'success'
        });
        this.$router.push({
          path:'/goodskind/list'
        })
          }
        })
      }
    }
}
</script>

