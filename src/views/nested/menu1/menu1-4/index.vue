<template>
  <div style="padding:30px;">
    <span class="tit">代收代支项目收入</span>
    <el-table
      :data="tableData"

      border
      style="width: 100%;"
    >
      <el-table-column
        prop="date"
        label="序号"
        width="80"
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
      tableData: []
    }
  }
}
</script>
<style >
