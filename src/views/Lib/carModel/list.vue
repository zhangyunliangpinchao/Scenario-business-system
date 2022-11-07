<template>
  <div class="content-offset">
    <el-breadcrumb>
      <el-breadcrumb-item :to="{ path: '/lib/carModel/list' }">首页</el-breadcrumb-item>
      <el-breadcrumb-item>基础库管理</el-breadcrumb-item>
    </el-breadcrumb>
    <div class="content" style="height: 800px">
      <el-row class="title">
        <el-col :span="18">
          <div class="grid-content bg-purple row-centre">
            <div class="title-font1">车型</div>
            <div class="title-font2">管理车型信息。可在该页面对车型进行新增、修改、删除操作。点击车型列表中车型名称可查看基础库详情。</div>
          </div>
        </el-col>
        <el-col :span="6">
          <div class="grid-content bg-purple row-centre" style="right: 40px">
            <el-button :disabled="state.multipleSelection.length === 0" @click="del()">删 除</el-button>
            <el-button type="primary" @click="toAdd">新 建</el-button>
          </div>
        </el-col>
      </el-row>
      <div style="height: 10px"></div>
      <el-table
        ref="multipleTableRef"
        class="table-content"
        :header-cell-style="{ background: '#fafafa', height: '50px', 'font-weight': '400', 'font-size': '16px' }"
        :row-style="{ height: '50px' }"
        :data="tableData"
        style="width: 100%"
        @selection-change="handleSelectionChange"
      >
        <el-table-column type="selection" width="65" align="right" />
        <el-table-column property="modelName" label="车型" min-width="120">
          <template #default="scoped">
            <el-button type="text" @click="toInfo(scoped.row)">{{ scoped.row.modelName }}</el-button>
          </template>
        </el-table-column>
      </el-table>
      <div class="pager">
        <el-pagination
          v-model:current-page="state.current"
          :page-size="state.pageSize"
          background
          layout="total,prev, pager, next,jumper"
          :total="state.total"
          @size-change="handleSizeChange"
          @current-change="handleCurrentChange"
        >
        </el-pagination>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
import { reactive, toRefs } from 'vue'
import router from '@/router'
import { store } from '@/store'

const state = reactive({
  multipleSelection: [] as any,
  tableData: [{ modelName: 'LIN-系列' }, { modelName: 'LIN-系列' }, { modelName: 'LIN-系列' }, { modelName: 'LIN-系列' }, { modelName: 'LIN-系列' }] as any, // 表格数据
  total: 10,
  pageSize: 10,
  current: 1,
  page: 1
})
const { tableData } = toRefs(state)

// 点击跳转新建
const toAdd = () => {
  router.push({
    path: '/lib/carModel/edit'
  })
}
// 点击跳转详情
const toInfo = (row: any) => {
  store.commit('setCarCache', {
    tabActive: 'carModel'
  })
  router.push({
    path: '/lib/carModel/info'
  })
}
const handleSelectionChange = (val: any) => {
  state.multipleSelection = val
}

const handleSizeChange = (val: number) => {
  state.pageSize = val
}
const handleCurrentChange = (val: number) => {
  state.current = val
}
</script>

<style>
@import '../../../assets/css/title.css';
@import '../../../assets/css/breadcrumb.css';
@import '../../../assets/css/table.css';
@import '../../../assets/css/row.css';
@import '../../../assets/css/content.css';
.container {
  color: black;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
.element-plus-logo {
  width: 50%;
}
.pager {
  margin-top: 20px;
  margin-bottom: 20px;
  display: flex;
  justify-content: center;
}
</style>
