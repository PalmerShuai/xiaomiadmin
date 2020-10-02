<template>
<el-form ref="form" :model="form" label-width="80px">
<el-form-item label="商品图片">
<el-upload
  class="avatar-uploader"
  action="uploadData"
  :http-request="UploadImage"
  :show-file-list="false"
  :on-success="handleAvatarSuccess"
  :before-upload="beforeAvatarUpload">
  <img v-if="imageUrl" :src="imageUrl" class="avatar">
  <i v-else class="el-icon-plus avatar-uploader-icon"></i>
</el-upload>
</el-form-item>
  <el-form-item label="商品名称">
    <el-input v-model="form.title"></el-input>
  </el-form-item>
   <el-form-item label="商品种类">
    <el-select v-model="form.region" placeholder="请选择商品种类">
      <el-option label="区域一" value="shanghai"></el-option>
      <el-option label="区域二" value="beijing"></el-option>
    </el-select>
  </el-form-item>
   <el-form-item label="商品价格">
    <el-input v-model="form.price"></el-input>
  </el-form-item>
   <el-form-item label="商品描述">
    <el-input v-model="form.desc"></el-input>
  </el-form-item>
  <el-form-item label="商品热度">
    <el-input v-model="form.hot"></el-input>
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
  name: 'CreateGoods',
  components: {  },
    data() {
    return {
imageUrl:'',
form:{
  name:'',
  title:'',
  desc:'',
price:'',
kind:'',
hot:''
},
    }
  },
  methods:{
      UploadImage(param) {
        let uploadData = new FormData();
        uploadData.append('avatar', param.file);
         // 上传图片的接口  传上去后让后台返回一个地址
        axios.post('/upload',uploadData).then(res=>{
          this.imageUrl=res.data.path
        })
      },
  handleAvatarSuccess(res, file) {
        this.imageUrl = URL.createObjectURL(file.raw);
        console.log(this.imageUrl)
      },
      beforeAvatarUpload(file) {
        const isJPG = file.type === 'image/jpeg';
        const isLt2M = file.size / 1024 / 1024 < 2;

        if (!isJPG) {
          this.$message.error('上传头像图片只能是 JPG 格式!');
        }
        if (!isLt2M) {
          this.$message.error('上传头像图片大小不能超过 2MB!');
        }
        return isJPG && isLt2M;
      },
       onSubmit() {
        console.log('submit!');
      }
    }
}
</script>

  }
}
</script>
<style scoped>
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
    line-height: 178px;
    text-align: center;
  }
  .avatar {
    width: 178px;
    height: 178px;
    display: block;
  }

</style>

