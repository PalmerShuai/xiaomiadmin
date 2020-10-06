<template>
 <el-table
    ref="singleTable"
    :data="carData"
    highlight-current-row
    @current-change="handleCurrentChange"
    style="width: 100%">
    <el-table-column
      type="index"
      width="50">
    </el-table-column>
    <el-table-column
      property="uid"
      label="用户id"
      width="120">
    </el-table-column>
    <el-table-column
      property="pid"
      label="商品id">
    </el-table-column>
    <el-table-column
      property="num"
      label="商品数量">
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
  name: 'UserList',
  components: { },
  filters: {

  },
  data() {
    return {
carData: [],
        currentRow: null

    }
  },
  created() {
this.getlist()
  },
  methods: {
    getlist(){
axios.get('/carList').then(res=>{
  if(res.data.code=20000){
    this.carData=res.data.list
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
        axios.delete('/carDele/'+id).then(res=>{
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
