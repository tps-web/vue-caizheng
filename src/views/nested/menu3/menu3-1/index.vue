<template>
  <div class="app-container">
    <el-button type="primary" :loading="downloadLoading" style="margin:0 0 20px 20px;" icon="el-icon-document" @click="handleDownload">
      导出
    </el-button>
    <el-button type="primary" @click="handleAddRole">添加</el-button>
    <el-table
      ref="multipleTable"
      height="500"
      :data="tableData.slice((currentPage-1)*pagesize,currentPage*pagesize)"
      tooltip-effect="dark"
      style="width: 100%"
      @selection-change="handleSelectionChange"
    >
      <el-table-column
        type="selection"
        width="55"
      />
      <el-table-column align="center" label="Id" width="95">
        <template slot-scope="scope">
          {{ scope.row.id }}
        </template>
      </el-table-column>
      <el-table-column
        label="日期"
        width="120"
      >
        <template slot-scope="scope">{{ scope.row.date }}</template>
      </el-table-column>
      <el-table-column
        prop="name"
        label="姓名"
        width="120"
      />
      <el-table-column
        prop="address"
        label="地址"
        show-overflow-tooltip
      />
      <el-table-column width="80">
        <template slot-scope="scope">
          <el-button type="primary" el-icon-delete size="small" @click="getid(scope.$index)">删除</el-button>
        </template>
      </el-table-column>
      <el-table-column>
        <template slot-scope="scope">
          <el-button el-icon-delete size="small" @click="editid(scope)">编辑</el-button>
        </template>
      </el-table-column>
    </el-table>

    <!-- edit -->
    <el-dialog :visible.sync="dialogVisible" :title="dialogType==='edit'?'Edit Role':'New Role'">
      <el-form :model="role" label-width="80px" label-position="left">
        <el-form-item label="id">
          <el-input v-model="role.id" disabled />
        </el-form-item>
        <el-form-item label="日期">
          <el-input v-model="role.date" placeholder="date" />
        </el-form-item>
        <el-form-item label="姓名">
          <el-input v-model="role.name" placeholder="name" />
        </el-form-item>
        <el-form-item label="Desc">
          <el-input
            v-model="role.address"
            type="textarea"
            placeholder="Role Description"
          />
        </el-form-item>
      </el-form>
      <div style="text-align:right;">
        <el-button type="danger" @click="dialogVisible=false">Cancel</el-button>
        <el-button type="primary" @click="confirmRole">Confirm</el-button>
      </div>
    </el-dialog>
    <el-pagination
      class="fy"
      layout="prev, pager, next"
      :total="total"
      background
      @current-change="current_change"
    />

  </div>
</template>

<script>
import { parseTime, deepClone } from '@/utils'
const defaultRole = {
  date: '',
  name: '',
  address: ''
}
export default {
  data() {
    return {
      role: Object.assign({}, defaultRole),
      downloadLoading: false,
      dialogVisible: false, // 模态框
      dialogType: 'new',
      total: 1000,
      currentPage: 1,
      pagesize: 10,
      tableData: [{
        id: 1,
        date: '2016-05-03',
        name: '王小虎1',
        address: '上海市普陀区金沙江路 1518 弄'
      }, {
        id: 2,
        date: '2016-05-02',
        name: '王小虎2',
        address: '上海市普陀区金沙江路 1518 弄'
      }, {
        id: 3,
        date: '2016-05-04',
        name: '王小虎3',
        address: '上海市普陀区金沙江路 1518 弄'
      }, {
        id: 4,
        date: '2016-05-01',
        name: '王小虎4',
        address: '上海市普陀区金沙江路 1518 弄'
      }, {
        id: 5,
        date: '2016-05-08',
        name: '王小虎5',
        address: '上海市普陀区金沙江路 1518 弄'
      }, {
        id: 6,
        date: '2016-05-06',
        name: '王小虎6',
        address: '上海市普陀区金沙江路 1518 弄'
      }, {
        id: 7,
        date: '2016-05-07',
        name: '王小虎7',
        address: '上海市普陀区金沙江路 1518 弄'
      },
      {
        id: 1,
        date: '2016-05-03',
        name: '王小虎1',
        address: '上海市普陀区金沙江路 1518 弄'
      }, {
        id: 2,
        date: '2016-05-02',
        name: '王小虎2',
        address: '上海市普陀区金沙江路 1518 弄'
      }, {
        id: 1,
        date: '2016-05-03',
        name: '王小虎1',
        address: '上海市普陀区金沙江路 1518 弄'
      }, {
        id: 2,
        date: '2016-05-02',
        name: '王小虎2',
        address: '上海市普陀区金沙江路 1518 弄'
      }, {
        id: 1,
        date: '2016-05-03',
        name: '王小虎1',
        address: '上海市普陀区金沙江路 1518 弄'
      }, {
        id: 2,
        date: '2016-05-02',
        name: '王小虎2',
        address: '上海市普陀区金沙江路 1518 弄'
      }, {
        id: 1,
        date: '2016-05-03',
        name: '王小虎1',
        address: '上海市普陀区金沙江路 1518 弄'
      }, {
        id: 2,
        date: '2016-05-02',
        name: '王小虎2',
        address: '上海市普陀区金沙江路 1518 弄'
      }, {
        id: 1,
        date: '2016-05-03',
        name: '王小虎1',
        address: '上海市普陀区金沙江路 1518 弄'
      }, {
        id: 2,
        date: '2016-05-02',
        name: '王小虎2',
        address: '上海市普陀区金沙江路 1518 弄'
      },
      {
        id: 1,
        date: '2016-05-03',
        name: '王小虎1',
        address: '上海市普陀区金沙江路 1518 弄'
      }, {
        id: 2,
        date: '2016-05-02',
        name: '王小虎2',
        address: '上海市普陀区金沙江路 1518 弄'
      }, {
        id: 1,
        date: '2016-05-03',
        name: '王小虎1',
        address: '上海市普陀区金沙江路 1518 弄'
      }, {
        id: 2,
        date: '2016-05-02',
        name: '王小虎2',
        address: '上海市普陀区金沙江路 1518 弄'
      }, {
        id: 1,
        date: '2016-05-03',
        name: '王小虎1',
        address: '上海市普陀区金沙江路 1518 弄'
      }, {
        id: 2,
        date: '2016-05-02',
        name: '王小虎2',
        address: '上海市普陀区金沙江路 1518 弄'
      }, {
        id: 3,
        date: '2016-05-04',
        name: '王小虎3',
        address: '上海市普陀区金沙江路 1518 弄'
      }, {
        id: 4,
        date: '2016-05-01',
        name: '王小虎4',
        address: '上海市普陀区金沙江路 1518 弄'
      }, {
        id: 5,
        date: '2016-05-08',
        name: '王小虎5',
        address: '上海市普陀区金沙江路 1518 弄'
      }, {
        id: 6,
        date: '2016-05-06',
        name: '王小虎6',
        address: '上海市普陀区金沙江路 1518 弄'
      }, {
        id: 7,
        date: '2016-05-07',
        name: '王小虎7',
        address: '上海市普陀区金沙江路 1518 弄'
      },
      {
        id: 1,
        date: '2016-05-03',
        name: '王小虎1',
        address: '上海市普陀区金沙江路 1518 弄'
      }, {
        id: 2,
        date: '2016-05-02',
        name: '王小虎2',
        address: '上海市普陀区金沙江路 1518 弄'
      }, {
        id: 1,
        date: '2016-05-03',
        name: '王小虎1',
        address: '上海市普陀区金沙江路 1518 弄'
      }, {
        id: 2,
        date: '2016-05-02',
        name: '王小虎2',
        address: '上海市普陀区金沙江路 1518 弄'
      }, {
        id: 1,
        date: '2016-05-03',
        name: '王小虎1',
        address: '上海市普陀区金沙江路 1518 弄'
      }, {
        id: 2,
        date: '2016-05-02',
        name: '王小虎2',
        address: '上海市普陀区金沙江路 1518 弄'
      }, {
        id: 1,
        date: '2016-05-03',
        name: '王小虎1',
        address: '上海市普陀区金沙江路 1518 弄'
      }, {
        id: 2,
        date: '2016-05-02',
        name: '王小虎2',
        address: '上海市普陀区金沙江路 1518 弄'
      }, {
        id: 1,
        date: '2016-05-03',
        name: '王小虎1',
        address: '上海市普陀区金沙江路 1518 弄'
      }, {
        id: 2,
        date: '2016-05-02',
        name: '王小虎2',
        address: '上海市普陀区金沙江路 1518 弄'
      },
      {
        id: 1,
        date: '2016-05-03',
        name: '王小虎1',
        address: '上海市普陀区金沙江路 1518 弄'
      }, {
        id: 2,
        date: '2016-05-02',
        name: '王小虎2',
        address: '上海市普陀区金沙江路 1518 弄'
      }, {
        id: 1,
        date: '2016-05-03',
        name: '王小虎1',
        address: '上海市普陀区金沙江路 1518 弄'
      }, {
        id: 2,
        date: '2016-05-02',
        name: '王小虎2',
        address: '上海市普陀区金沙江路 1518 弄'
      }, {
        id: 1,
        date: '2016-05-03',
        name: '王小虎1',
        address: '上海市普陀区金沙江路 1518 弄'
      }, {
        id: 2,
        date: '2016-05-02',
        name: '王小虎2',
        address: '上海市普陀区金沙江路 1518 弄'
      }, {
        id: 3,
        date: '2016-05-04',
        name: '王小虎3',
        address: '上海市普陀区金沙江路 1518 弄'
      }, {
        id: 4,
        date: '2016-05-01',
        name: '王小虎4',
        address: '上海市普陀区金沙江路 1518 弄'
      }, {
        id: 5,
        date: '2016-05-08',
        name: '王小虎5',
        address: '上海市普陀区金沙江路 1518 弄'
      }, {
        id: 6,
        date: '2016-05-06',
        name: '王小虎6',
        address: '上海市普陀区金沙江路 1518 弄'
      }, {
        id: 7,
        date: '2016-05-07',
        name: '王小虎7',
        address: '上海市普陀区金沙江路 1518 弄'
      },
      {
        id: 1,
        date: '2016-05-03',
        name: '王小虎1',
        address: '上海市普陀区金沙江路 1518 弄'
      }, {
        id: 2,
        date: '2016-05-02',
        name: '王小虎2',
        address: '上海市普陀区金沙江路 1518 弄'
      }, {
        id: 1,
        date: '2016-05-03',
        name: '王小虎1',
        address: '上海市普陀区金沙江路 1518 弄'
      }, {
        id: 2,
        date: '2016-05-02',
        name: '王小虎2',
        address: '上海市普陀区金沙江路 1518 弄'
      }, {
        id: 1,
        date: '2016-05-03',
        name: '王小虎1',
        address: '上海市普陀区金沙江路 1518 弄'
      }, {
        id: 2,
        date: '2016-05-02',
        name: '王小虎2',
        address: '上海市普陀区金沙江路 1518 弄'
      }, {
        id: 1,
        date: '2016-05-03',
        name: '王小虎1',
        address: '上海市普陀区金沙江路 1518 弄'
      }, {
        id: 2,
        date: '2016-05-02',
        name: '王小虎2',
        address: '上海市普陀区金沙江路 1518 弄'
      }, {
        id: 1,
        date: '2016-05-03',
        name: '王小虎1',
        address: '上海市普陀区金沙江路 1518 弄'
      }, {
        id: 2,
        date: '2016-05-02',
        name: '王小虎2',
        address: '上海市普陀区金沙江路 1518 弄'
      },
      {
        id: 1,
        date: '2016-05-03',
        name: '王小虎1',
        address: '上海市普陀区金沙江路 1518 弄'
      }, {
        id: 2,
        date: '2016-05-02',
        name: '王小虎2',
        address: '上海市普陀区金沙江路 1518 弄'
      }, {
        id: 1,
        date: '2016-05-03',
        name: '王小虎1',
        address: '上海市普陀区金沙江路 1518 弄'
      }, {
        id: 2,
        date: '2016-05-02',
        name: '王小虎2',
        address: '上海市普陀区金沙江路 1518 弄'
      }, {
        id: 1,
        date: '2016-05-03',
        name: '王小虎1',
        address: '上海市普陀区金沙江路 1518 弄'
      }, {
        id: 2,
        date: '2016-05-02',
        name: '王小虎2',
        address: '上海市普陀区金沙江路 1518 弄'
      }, {
        id: 3,
        date: '2016-05-04',
        name: '王小虎3',
        address: '上海市普陀区金沙江路 1518 弄'
      }, {
        id: 4,
        date: '2016-05-01',
        name: '王小虎4',
        address: '上海市普陀区金沙江路 1518 弄'
      }, {
        id: 5,
        date: '2016-05-08',
        name: '王小虎5',
        address: '上海市普陀区金沙江路 1518 弄'
      }, {
        id: 6,
        date: '2016-05-06',
        name: '王小虎6',
        address: '上海市普陀区金沙江路 1518 弄'
      }, {
        id: 7,
        date: '2016-05-07',
        name: '王小虎7',
        address: '上海市普陀区金沙江路 1518 弄'
      },
      {
        id: 1,
        date: '2016-05-03',
        name: '王小虎1',
        address: '上海市普陀区金沙江路 1518 弄'
      }, {
        id: 2,
        date: '2016-05-02',
        name: '王小虎2',
        address: '上海市普陀区金沙江路 1518 弄'
      }, {
        id: 1,
        date: '2016-05-03',
        name: '王小虎1',
        address: '上海市普陀区金沙江路 1518 弄'
      }, {
        id: 2,
        date: '2016-05-02',
        name: '王小虎2',
        address: '上海市普陀区金沙江路 1518 弄'
      }, {
        id: 1,
        date: '2016-05-03',
        name: '王小虎1',
        address: '上海市普陀区金沙江路 1518 弄'
      }, {
        id: 2,
        date: '2016-05-02',
        name: '王小虎2',
        address: '上海市普陀区金沙江路 1518 弄'
      }, {
        id: 1,
        date: '2016-05-03',
        name: '王小虎1',
        address: '上海市普陀区金沙江路 1518 弄'
      }, {
        id: 2,
        date: '2016-05-02',
        name: '王小虎2',
        address: '上海市普陀区金沙江路 1518 弄'
      }, {
        id: 1,
        date: '2016-05-03',
        name: '王小虎1',
        address: '上海市普陀区金沙江路 1518 弄'
      }, {
        id: 2,
        date: '2016-05-02',
        name: '王小虎2',
        address: '上海市普陀区金沙江路 1518 弄'
      },
      {
        id: 1,
        date: '2016-05-03',
        name: '王小虎1',
        address: '上海市普陀区金沙江路 1518 弄'
      }, {
        id: 2,
        date: '2016-05-02',
        name: '王小虎2',
        address: '上海市普陀区金沙江路 1518 弄'
      }, {
        id: 1,
        date: '2016-05-03',
        name: '王小虎1',
        address: '上海市普陀区金沙江路 1518 弄'
      }, {
        id: 2,
        date: '2016-05-02',
        name: '王小虎2',
        address: '上海市普陀区金沙江路 1518 弄'
      }, {
        id: 1,
        date: '2016-05-03',
        name: '王小虎1',
        address: '上海市普陀区金沙江路 1518 弄'
      }, {
        id: 2,
        date: '2016-05-02',
        name: '王小虎2',
        address: '上海市普陀区金沙江路 1518 弄'
      }, {
        id: 3,
        date: '2016-05-04',
        name: '王小虎3',
        address: '上海市普陀区金沙江路 1518 弄'
      }, {
        id: 4,
        date: '2016-05-01',
        name: '王小虎4',
        address: '上海市普陀区金沙江路 1518 弄'
      }, {
        id: 5,
        date: '2016-05-08',
        name: '王小虎5',
        address: '上海市普陀区金沙江路 1518 弄'
      }, {
        id: 6,
        date: '2016-05-06',
        name: '王小虎6',
        address: '上海市普陀区金沙江路 1518 弄'
      }, {
        id: 7,
        date: '2016-05-07',
        name: '王小虎7',
        address: '上海市普陀区金沙江路 1518 弄'
      },
      {
        id: 1,
        date: '2016-05-03',
        name: '王小虎1',
        address: '上海市普陀区金沙江路 1518 弄'
      }, {
        id: 2,
        date: '2016-05-02',
        name: '王小虎2',
        address: '上海市普陀区金沙江路 1518 弄'
      }, {
        id: 1,
        date: '2016-05-03',
        name: '王小虎1',
        address: '上海市普陀区金沙江路 1518 弄'
      }, {
        id: 2,
        date: '2016-05-02',
        name: '王小虎2',
        address: '上海市普陀区金沙江路 1518 弄'
      }, {
        id: 1,
        date: '2016-05-03',
        name: '王小虎1',
        address: '上海市普陀区金沙江路 1518 弄'
      }, {
        id: 2,
        date: '2016-05-02',
        name: '王小虎2',
        address: '上海市普陀区金沙江路 1518 弄'
      }, {
        id: 1,
        date: '2016-05-03',
        name: '王小虎1',
        address: '上海市普陀区金沙江路 1518 弄'
      }, {
        id: 2,
        date: '2016-05-02',
        name: '王小虎2',
        address: '上海市普陀区金沙江路 1518 弄'
      }, {
        id: 1,
        date: '2016-05-03',
        name: '王小虎1',
        address: '上海市普陀区金沙江路 1518 弄'
      }, {
        id: 2,
        date: '2016-05-02',
        name: '王小虎2',
        address: '上海市普陀区金沙江路 1518 弄'
      },
      {
        id: 1,
        date: '2016-05-03',
        name: '王小虎1',
        address: '上海市普陀区金沙江路 1518 弄'
      }, {
        id: 2,
        date: '2016-05-02',
        name: '王小虎2',
        address: '上海市普陀区金沙江路 1518 弄'
      }, {
        id: 1,
        date: '2016-05-03',
        name: '王小虎1',
        address: '上海市普陀区金沙江路 1518 弄'
      }, {
        id: 2,
        date: '2016-05-02',
        name: '王小虎2',
        address: '上海市普陀区金沙江路 1518 弄'
      }, {
        id: 1,
        date: '2016-05-03',
        name: '王小虎1',
        address: '上海市普陀区金沙江路 1518 弄'
      }, {
        id: 2,
        date: '2016-05-02',
        name: '王小虎2',
        address: '上海市普陀区金沙江路 1518 弄'
      }, {
        id: 3,
        date: '2016-05-04',
        name: '王小虎3',
        address: '上海市普陀区金沙江路 1518 弄'
      }, {
        id: 4,
        date: '2016-05-01',
        name: '王小虎4',
        address: '上海市普陀区金沙江路 1518 弄'
      }, {
        id: 5,
        date: '2016-05-08',
        name: '王小虎5',
        address: '上海市普陀区金沙江路 1518 弄'
      }, {
        id: 6,
        date: '2016-05-06',
        name: '王小虎6',
        address: '上海市普陀区金沙江路 1518 弄'
      }, {
        id: 7,
        date: '2016-05-07',
        name: '王小虎7',
        address: '上海市普陀区金沙江路 1518 弄'
      },
      {
        id: 1,
        date: '2016-05-03',
        name: '王小虎1',
        address: '上海市普陀区金沙江路 1518 弄'
      }, {
        id: 2,
        date: '2016-05-02',
        name: '王小虎2',
        address: '上海市普陀区金沙江路 1518 弄'
      }, {
        id: 1,
        date: '2016-05-03',
        name: '王小虎1',
        address: '上海市普陀区金沙江路 1518 弄'
      }, {
        id: 2,
        date: '2016-05-02',
        name: '王小虎2',
        address: '上海市普陀区金沙江路 1518 弄'
      }, {
        id: 1,
        date: '2016-05-03',
        name: '王小虎1',
        address: '上海市普陀区金沙江路 1518 弄'
      }, {
        id: 2,
        date: '2016-05-02',
        name: '王小虎2',
        address: '上海市普陀区金沙江路 1518 弄'
      }, {
        id: 1,
        date: '2016-05-03',
        name: '王小虎1',
        address: '上海市普陀区金沙江路 1518 弄'
      }, {
        id: 2,
        date: '2016-05-02',
        name: '王小虎2',
        address: '上海市普陀区金沙江路 1518 弄'
      }, {
        id: 1,
        date: '2016-05-03',
        name: '王小虎1',
        address: '上海市普陀区金沙江路 1518 弄'
      }, {
        id: 2,
        date: '2016-05-02',
        name: '王小虎2',
        address: '上海市普陀区金沙江路 1518 弄'
      },
      {
        id: 1,
        date: '2016-05-03',
        name: '王小虎1',
        address: '上海市普陀区金沙江路 1518 弄'
      }, {
        id: 2,
        date: '2016-05-02',
        name: '王小虎2',
        address: '上海市普陀区金沙江路 1518 弄'
      }, {
        id: 1,
        date: '2016-05-03',
        name: '王小虎1',
        address: '上海市普陀区金沙江路 1518 弄'
      }, {
        id: 2,
        date: '2016-05-02',
        name: '王小虎2',
        address: '上海市普陀区金沙江路 1518 弄'
      }],
      multipleSelection: []
    }
  },

  created: function() {
    this.total = this.tableData.length
  },
  methods: {
    confirmRole() {
      if (this.dialogType === 'new') {
        console.log(this.tableData.length + 1)
        this.role.id = this.tableData.length + 1
        this.tableData.push(this.role)
        this.$message('添加成功')
        this.dialogVisible = false
      } else {
        // console.log(this.role.id)
        const id = this.role.id - 1
        this.tableData.splice(id, 1, this.role)
        this.$message('编辑成功')
        this.dialogVisible = false
      }
    },

    current_change(currentPage) {
      console.log(`当前页: ${currentPage}`)
      this.currentPage = currentPage
    },
    editid(scope) {
      this.dialogType = 'edit'
      this.dialogVisible = true
      // console.log(scope)
      this.role = deepClone(scope.row) // 深拷贝
      // console.log(this.role)
    },
    // add
    handleAddRole() {
      this.role = Object.assign({}, defaultRole) // 浅拷贝
      this.role.id = this.tableData.length + 1
      this.dialogType = 'new'
      this.dialogVisible = true
    },
    toggleSelection(rows) {
      if (rows) {
        rows.forEach(row => {
          this.$refs.multipleTable.toggleRowSelection(row)
        })
      } else {
        this.$refs.multipleTable.clearSelection()
      }
    },
    handleSelectionChange(val) {
      this.multipleSelection = val
    },
    handleDownload() {
      this.downloadLoading = true
     import('@/vendor/Export2Excel').then(excel => {
       const tHeader = ['date', 'name', 'address']
       const filterVal = ['date', 'name', 'address']
       const list = this.tableData
       const data = this.formatJson(filterVal, list)
       excel.export_json_to_excel({
         header: tHeader, // 表头 必填
         data, // 具体数据 必填
         filename: 'excel-list', // 非必填
         autoWidth: true, // 非必填
         bookType: 'xlsx' // 非必填

       })
       this.downloadLoading = false
     })
    },
    formatJson(filterVal, jsonData) {
      return jsonData.map(v => filterVal.map(j => {
        if (j === 'timestamp') {
          return parseTime(v[j])
        } else {
          return v[j]
        }
      }))
    },
    getid(id) {
      console.log(id)
      this.tableData.splice(id, 1)
    }
  }
}
</script>

<style scoped>

 .fy{
        text-align:center;
        margin-top:30px;
    }
</style>

