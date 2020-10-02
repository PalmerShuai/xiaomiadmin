<template>
 <el-table
    ref="singleTable"
    :data="goodskindData"
    highlight-current-row
    @current-change="handleCurrentChange"
    style="width: 100%">
    <el-table-column
      type="index"
      width="50">
    </el-table-column>
    <el-table-column
      property="username"
      label="商品种类名"
      width="120">
    </el-table-column>
    <el-table-column label="操作">
      <template slot-scope="scope">
        <el-button
          size="mini"
          @click="handleEdit(scope.row._id)">编辑</el-button>
        <el-button
          size="mini"
          type="danger"
          @click="handleDelete(scope.row._id)">删除</el-button>
      </template>
    </el-table-column>
  </el-table>

</template>

<script>
// Secondary package based on el-pagination
import axios from 'axios'
export default {
  name: 'GoodskindList',
  components: { },
  filters: {

  },
  data() {
    return {
goodskindData: [],
        currentRow: null

    }
  },
  created() {
this.getlist()
  },
  methods: {
    getlist(){
axios.get('/userList').then(res=>{
  if(res.data.code=20000){
    this.goodskindData=res.data.list
  }
})
    },
handleCurrentChange(val) {
        this.currentRow = val;
      },
       handleEdit(id) {
        this.$router.push({
          path:'edit/'+id
        })
      },
      handleDelete(id) {
        axios.delete('/userDele/'+id).then(res=>{
           if(res.data.code=20000){
             this.getlist();
             this.$message({
          showClose: true,
          message: res.data.msg,
          type: 'success'
        });
           }
        })
      }
  }
}
</script>

<style scoped>

</style>
