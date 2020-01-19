<template>
  <div class="dashboard-container">
    <!-- topbtn -->
    <div class="demo-input-suffix fl" size="small">
      <el-select v-model="value" placeholder="请选择">
        <el-option
          v-for="item in options"
          :key="item.id"
          :value="item.label"
        />
      </el-select>
      <el-select v-model="value1" placeholder="请选择">
        <el-option
          v-for="item in yue"
          :key="item.id"
          :value="item.label"
        />
      </el-select>
      <el-button type="primary" size="small" @click="tijiao">查询</el-button>
      <el-button type="primary" size="small">新增</el-button>
      <el-button type="primary" size="small">导出</el-button>
    </div>
    <!-- table -->
    <template>
      <el-table
        class="tableBox"
        :data="tableData"
        height="550"
        border
        :header-cell-style="{background:'#eef1f6',border:'1px solid #ccc' }"
        style="width: 100%; padding:30px"
      >
        <el-table-column label="日期" align="center">
          <el-table-column
            prop="month"
            label="月"
            width="80"
            align="center"
          />
          <el-table-column
            prop="day"
            label="日"
            width="80"
            align="center"
          />
        </el-table-column>
        <el-table-column
          prop="serial"
          label="序号"
          width="100"
          align="center"
        />
        <el-table-column label="凭证" align="center">
          <el-table-column
            prop="type"
            align="center"
            label="类型"
            width="80"
          />
          <el-table-column
            prop="number"
            label="编号"
            width="80"
          />
        </el-table-column>
        <el-table-column
          prop="abstract"
          label="摘要"
          width="120"
          align="center"
        />
        <el-table-column label="凭证" align="center">
          <el-table-column
            prop="cash"
            label="现金"
            width="80"
            align="center"
          />
          <el-table-column
            prop="debite"
            label="借方金额"
            width="80"
            align="center"
          />
          <el-table-column
            prop="aocs"
            label="贷方金额	"
            width="80"
            align="center"
          />
          <el-table-column
            prop="direction"
            label="方向"
            align="center"

            width="80"
          />
          <el-table-column
            prop="balance"
            label="当前余额"
            width="80"
            align="center"
          />
        </el-table-column>
        <el-table-column
          prop="Bill"
          label="票据号"
          align="center"

          width="120"
        />
      </el-table>
    </template>
  </div>

</template>

<script>

export default {
  data() {
    return {
      tableData: [
        {
          month: 1,
          day: 2,
          serial: '3',
          type: '4',
          number: '5',
          abstract: '6',
          cash: '7',
          debite: '7.1',
          aocs: '8',
          direction: '9',
          balance: '10',
          Bill: '11'
        },
        {
          month: 1,
          day: 2,
          serial: '3',
          type: '4',
          number: '5',
          abstract: '6',
          cash: '7',
          debite: '7.1',
          aocs: '8',
          direction: '9',
          balance: '10',
          Bill: '11'
        },
        {
          month: 1,
          day: 2,
          serial: '3',
          type: '4',
          number: '5',
          abstract: '6',
          cash: '7',
          debite: '7.1',
          aocs: '8',
          direction: '9',
          balance: '10',
          Bill: '11'
        }
      ],
      value: '',
      value1: '',
      options: [
        {
          label: '选项1',
          id: 1
        },
        {
          label: '选项2',
          id: 2

        },
        {
          label: '选项3',
          id: 3

        }, {
          label: '选项4',
          id: 4
        }
      ],
      yue: [
        {
          label: '1月',
          id: 1
        },
        {
          label: '2月',
          id: 2

        },
        {
          label: '3月',
          id: 3

        }, {
          label: '4月',
          id: 4
        }]
    }
  },
  methods: {
    tijiao() {
      console.log(this.value)
      console.log(this.value1)
    }
  }
}
</script>

<style scoped>
.fl{
  float: right;
  margin-top: 20px;
  margin-right: 100px;
}

</style>
