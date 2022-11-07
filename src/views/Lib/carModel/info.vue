<template>
  <div class="content-offset">
    <el-breadcrumb>
      <el-breadcrumb-item :to="{ path: '/lib/carModel/list' }">首页</el-breadcrumb-item>

      <el-breadcrumb-item :to="{ path: '/lib/carModel/list' }">基础库管理</el-breadcrumb-item>
      <el-breadcrumb-item>基础库详情</el-breadcrumb-item>
    </el-breadcrumb>
    <div class="content">
      <el-row class="title2 title-background title-border">
        <el-col :span="24">
          <div class="grid-content bg-purple row-centre">
            <div class="title-font1">车型详情</div>
          </div>
        </el-col>
      </el-row>
      <el-descriptions :column="2" :size="small" direction="vertical">
        <el-descriptions-item width="50%" label="车型名称">{{ 3 }}</el-descriptions-item>
        <el-descriptions-item width="50%" label="原子服务能力总数">{{ 3 }}</el-descriptions-item>
        <el-descriptions-item label="车辆总数">{{ 3 }}</el-descriptions-item>
        <el-descriptions-item label="已发布场景数量">{{ 3 }} </el-descriptions-item>
      </el-descriptions>
    </div>
    <!-- 标签页 start -->
    <el-tabs v-model="activeName" style="background-color: #f5f7fa; margin-left: 20px" @tab-click="tabChange">
      <!-- 车型信息 start -->
      <el-tab-pane class="pane1" name="carModel">
        <template #label><span>车型信息</span> </template>
        <el-row class="title title-background title-border">
          <el-col :span="24">
            <div class="grid-content bg-purple row-centre">
              <div class="title-font1">车型信息</div>
              <div class="title-font2">可查看该车型下车辆信息。</div>
            </div>
          </el-col>
        </el-row>
        <el-row style="height: 100px">
          <el-col :span="12">
            <div class="grid-content bg-purple row-centre">
              <div class="serch">
                <el-input v-model="carModelQuery.vinOrNumber" style="width: 300px" placeholder="输入VIN码/车牌号搜索车辆" />
                <el-button class="searchBtn" @click="carModelSearch()"></el-button>
              </div>
            </div>
          </el-col>
          <el-col :span="12">
            <div class="grid-content bg-purple row-centre" style="right: 40px">
              <el-button type="primary" @click="carModelSync()">同 步</el-button>
            </div>
          </el-col>
        </el-row>
        <el-table :data="carModels" :header-cell-style="{ background: '#fafafa', height: '50px', 'font-weight': '400', 'font-size': '16px' }" :row-style="{ height: '50px' }">
          <el-table-column label="序号" type="index" width="200" align="center" />
          <el-table-column prop="vin" label="车牌VIN码" width="500" align="center" />
          <el-table-column prop="vehicleNumber" label="车牌号" width="500" align="center" />
          <el-table-column prop="vin" label="场景" width="400" align="center">
            <template #default="scoped">
              <el-popover :width="400" trigger="click">
                <template #reference>
                  <el-button type="text" @click="getScene(scoped.row)">查看场景</el-button>
                </template>
                <el-table :data="scenes">
                  <el-table-column property="name" label="场景列表"></el-table-column>
                </el-table>
              </el-popover>
            </template>
          </el-table-column>
        </el-table>
        <div class="pager">
          <el-pagination
            v-model:page-size="carModelQuery.size"
            v-model:current-page="carModelQuery.current"
            background
            :pager-count="7"
            layout="total,prev, pager, next,jumper"
            :total="carModelQuery.total"
            @size-change="handleSizeChange"
            @current-change="carModelSearch"
          >
          </el-pagination>
        </div>
      </el-tab-pane>
      <!-- 车型信息 end -->
      <!-- 服务库 start -->
      <el-tab-pane class="pane" name="service">
        <template #label><span class="span"> 服务库</span></template>
        <el-row class="title title-background title-border">
          <el-col :span="24">
            <div class="grid-content bg-purple row-centre">
              <div class="title-font1">服务库</div>
              <div class="title-font2">可查看该车型下服务列表。点击新建，进入服务新建/导入页面。</div>
            </div>
          </el-col>
        </el-row>
      </el-tab-pane>
      <!-- 服务库 end -->
    </el-tabs>
    <!-- 标签页结束 -->
  </div>
</template>

<script setup lang="ts">
import { reactive, toRefs } from 'vue'

const state = reactive({
  activeName: 'carModel',
  carModelQuery: {
    current: 1,
    size: 10,
    total: 0,
    vinOrNumber: ''
  }, // 车型信息搜索条件
  carModels: [
    { vehicleNumber: '12312333', vin: '沪nb33' },
    { vehicleNumber: '12312333', vin: '沪nb33' }
  ] as any, // 车型信息表格
  scenes: [{ name: '灯光秀场景' }, { name: '灯光秀场景' }, { name: '灯光秀场景' }] as any
})
const { activeName, carModelQuery, carModels, scenes } = toRefs(state)
</script>

<style scoped>
@import '../../../assets/css/breadcrumb.css';
@import '../../../assets/css/title.css';
@import '../../../assets/css/table.css';
@import '../../../assets/css/row.css';
@import '../../../assets/css/content.css';
@import '../../../assets/css/serch.css';
.container {
  color: black;
}
.span {
  padding-right: 35px;
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
.el-input >>> .el-input__inner {
  height: 40px;
  line-height: 40px;
}

/* .shadow_border {
  border: 1px solid rgba(0, 0, 0, 0.05);
  box-shadow: 0 4px 1px 0px rgba(0, 0, 0, 0.05);
} */
.el-tabs >>> #tab-carModel,
.el-tabs >>> #tab-service,
.el-tabs >>> #tab-touch,
.el-tabs >>> #tab-model {
  border-right: 2px solid #e2e2e3;
  margin-bottom: 6px;
}

/* .el-tabs >>> #tab-carModel{
    padding: 0px 36px;
} */
.el-tabs >>> .el-tabs__item {
  padding: 0px 36px;
}

.el-table--fit {
  padding: 0px !important;
}

.el-tabs >>> .el-tabs__item span {
  font-size: 18px;
  font-weight: 500;
  line-height: 14px;
  color: #666666;
}

.el-tabs >>> .is-active span {
  color: #1d5adf !important;
}

.el-tabs >>> .el-tabs__header {
  margin-top: 4px;
  padding-top: 50px;
}

.el-tabs >>> .el-table {
  padding: 0px 30px;
}

.el-descriptions {
  margin-top: 20px;
  padding: 0px 40px;
}

.el-descriptions >>> .el-descriptions__label {
  height: 40px;
  color: #666666;
  font-weight: 400;
  font-size: 18px;
}

.el-descriptions >>> .el-descriptions__content {
  color: #000000;
  font-weight: 400;
  font-size: 18px;
}

.el-tabs >>> .el-tabs__content {
  background-color: rgba(255, 255, 255, 1);
  border-radius: 15px;
  box-shadow: rgba(0, 0, 0, 0.05) 0px 2px 2px 0px;
}
.pager {
  margin-top: 20px;
  margin-bottom: 20px;
  display: flex;
  justify-content: center;
}
</style>
