<template>
<el-form ref="form" :model="form" label-width="80px">
  <el-form-item label="用户id">
    <el-input v-model="form.uid"></el-input>
  </el-form-item>
  <el-form-item label="商品id">
    <el-input v-model="form.pid"></el-input>
  </el-form-item>
  <el-form-item label="商品数量">
    <el-input v-model="form.num"></el-input>
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
          uid: '',
          pis:'',
          num:''
        }
      }
    },
     methods: {
      onSubmit() {
        axios.post('/carsave',{
         uid: this.form.uid,
          pid:this.form.pid,
          num:this.form.num
        }).then(res=>{
          if(res.data.code=20000){
            this.$message({
          message: res.data.msg,
          type: 'success'
        });
        this.$router.push({
          path:'/car/list'
        })
          }
        })
      }
    }
}
</script>

