<template>
<el-form ref="form" :model="form" label-width="80px">
  <el-form-item label="用户名称">
    <el-input v-model="form.username"></el-input>
  </el-form-item>
  <el-form-item label="用户密码">
    <el-input v-model="form.password"></el-input>
  </el-form-item>
   <el-form-item>
    <el-button type="primary" @click="onSubmit(form._id)">立即修改</el-button>
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
          username: '',
          password:'',
          _id:''
        }
      }
    },
    created(){
this.showdata()
    },
     methods: {
       showdata(){
         const id =this.$route.params.id;
         axios.get('/showdata/'+id).then(res=>{
           if(res.data.code=20000){
             this.form=res.data.list
           }
         })

       },
      onSubmit(id) {

        axios.put('/uesruple/'+id,{
         username: this.form.username,
          password:this.form.password
        }).then(res=>{
          if(res.data.code=20000){
            this.$message({
          message: res.data.msg,
          type: 'success'
        });
        this.$router.push({
          path:'/user/list'
        })
          }
        })
      }
    }
}
</script>

