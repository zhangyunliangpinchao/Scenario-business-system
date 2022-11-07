<template>
  <div class="content-offset">
    <el-breadcrumb>
      <el-breadcrumb-item :to="{ path: '/lib/carModel/list' }">首页</el-breadcrumb-item>

      <el-breadcrumb-item :to="{ path: '/lib/carModel/list' }">基础库管理</el-breadcrumb-item>
      <el-breadcrumb-item>新建车型</el-breadcrumb-item>
    </el-breadcrumb>
    <div class="content" style="height: 800px">
      <el-row class="title">
        <el-col :span="18">
          <div class="grid-content bg-purple row-centre">
            <div class="title-font1">新建车型</div>
          </div>
        </el-col>
        <el-col :span="6">
          <div class="grid-content bg-purple row-centre" style="right: 40px">
            <el-button type="primary" @click="validate('formRef')">保 存</el-button>
          </div>
        </el-col>
      </el-row>
      <el-form ref="formRef" :model="carModel" label-position="left" style="width: 400px; padding-left: 40px" label-width="110px">
        <el-form-item label="车型代码" class="item-font1" prop="modelCode" :rules="{ required: true, message: '请输入车型代码', trigger: 'blur' }">
          <el-input v-model="carModel.modelCode"></el-input>
        </el-form-item>
        <el-form-item label="车型名称" class="item-font1" prop="modelName" :rules="{ required: true, message: '请输入车型名称', trigger: 'blur' }">
          <el-input v-model="carModel.modelName"></el-input>
        </el-form-item>
      </el-form>
    </div>
  </div>
</template>

<script setup lang="ts">
import { reactive, toRefs } from 'vue'

const state = reactive({
  carModel: {
    modelCode: '',
    modelName: ''
  }
})
const { carModel } = toRefs(state)
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
