<template>
  <div>

    <span class="tit">一般性转移支付</span>
    <el-table
      :data="tableData"
      height="600"
      border
      style="width: 100%;"
      highlight-current-row
    >
      <el-table-column
        prop="date"
        label="序号"
        width="80"
        fixed
        align="center"
      />
      <el-table-column
        prop="name"
        label="排序"
        width="80"
        align="center"
      />
      <el-table-column
        prop="address"
        label="项目名称"
        align="center"
      />
      <el-table-column
        prop="address"
        label="上报数"
        align="center"
      />
      <el-table-column
        prop="address"
        label="审核数"
        align="center"
      />
      <el-table-column
        prop="address"
        label="上年预算数"
        align="center"
      />
      <el-table-column
        prop="address"
        label="上年决算数"
        align="center"
      />
      <el-table-column
        prop="address"
        label="增减率"
        align="center"
      />
      <el-table-column
        prop="address"
        label="收入科目"
        align="center"
      />
      <el-table-column
        prop="address"
        label="收入类型"
        align="center"
      />
      <el-table-column
        prop="address"
        label="附件"
        align="center"
      />
      <el-table-column
        prop="address"
        label="操作"
        align="center"
      />
    </el-table>
  </div>
</template>
<script>
export default {
  data() {
    return {
      tableData: [{
        date: '2016-05-03',
        name: '王小虎',
        address: '上海市普陀区金沙江路 1518 弄'
      }, {
        date: '2016-05-02',
        name: '王小虎',
        address: '上海市普陀区金沙江路 1518 弄'
      }, {
        date: '2016-05-04',
        name: '王小虎',
        address: '上海市普陀区金沙江路 1518 弄'
      }, {
        date: '2016-05-01',
        name: '王小虎',
        address: '上海市普陀区金沙江路 1518 弄'
      }, {
        date: '2016-05-08',
        name: '王小虎',
        address: '上海市普陀区金沙江路 1518 弄'
      }, {
        date: '2016-05-06',
        name: '王小虎',
        address: '上海市普陀区金沙江路 1518 弄'
      }, {
        date: '2016-05-07',
        name: '王小虎',
        address: '上海市普陀区金沙江路 1518 弄'
      }, {
        date: '2016-05-07',
        name: '王小虎',
        address: '上海市普陀区金沙江路 1518 弄'
      }, {
        date: '2016-05-07',
        name: '王小虎',
        address: '上海市普陀区金沙江路 1518 弄'
      }, {
        date: '2016-05-07',
        name: '王小虎',
        address: '上海市普陀区金沙江路 1518 弄'
      }]
    }
  }
}
</script>
<style >
.tit{
  color:#304156;
  display: block;
  text-align: center;
  font-weight: bold;
  margin-bottom: 20px;
  font-size: 18px;
}
</style>
