<template>
  <el-table
    ref="singleTable"
    :data="tableData"
    highlight-current-row
    @current-change="handleCurrentChange"
    style="width: 100%"
  >
    <el-table-column type="index" width="50"></el-table-column>
    <el-table-column property="title" label="商品名称" width="120"></el-table-column>
    <el-table-column property="price" label="价格" width="120"></el-table-column>
    <el-table-column property="desc" label="描述"></el-table-column>
    <el-table-column property="hot" label="热度"></el-table-column>
    <el-table-column property="imgurl" label="图片">
    <template   slot-scope="scope">
                    <img :src="scope.row.imgurl"  min-width="70" height="70" />
                 </template>
    </el-table-column>
    <el-table-column label="操作">
      <template slot-scope="scope">
        <el-button size="mini" @click="handleEdit(scope.row._id)">编辑</el-button>
        <el-button size="mini" type="danger" @click="handleDelete(scope.row._id)">删除</el-button>
      </template>
    </el-table-column>
  </el-table>
</template>

<script>
import axios from "axios";
export default {
  name: "GoodsList",
  components: {},
  filters: {},
  data() {
    return {
      tableData: [],
    };
  },
  created() {
    this.getdatalist();
  },
  methods: {
    getdatalist() {
      axios.get("/getgoodslist").then(res => {
        this.tableData=res.data.list
      });
    },
    setCurrent(row) {
        this.$refs.singleTable.setCurrentRow(row);
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
         axios.delete('/goods/'+id).then(res=>{
this.getdatalist();
         })
      }
  },
};
</script>

<style scoped>
</style>
