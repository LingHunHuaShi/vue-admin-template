<template>
  <div class="dashboard-container">
    <el-row class="dashboard-row" :gutter="20">
      <el-col class="dashboard-col" :span="12">
        <el-card class="box-card">
          <div slot="header">
            <span>运行中的算法</span>
          </div>
          <div class="content-box">
            <span class="content">1个</span>
            <el-icon class="el-icon-office-building icon" />
          </div>
        </el-card>
      </el-col>
      <el-col class="dashboard-col" :span="12">
        <el-card class="box-card">
          <div slot="header">
            <span>内存占用</span>
          </div>
          <div class="content-box">
            <span class="content">3.2G / 4G</span>
            <el-icon class="iconfont icon-neicun icon" />
          </div>
        </el-card>
      </el-col>
    </el-row>

    <el-row class="dashboard-row" :gutter="20">
      <el-col class="dashboard-col" :span="12">
        <el-card class="box-card">
          <div slot="header">
            <span>CPU占用</span>
          </div>
          <div class="content-box">
            <span class="content">45%</span>
            <el-icon class="iconfont icon-cpu icon" />
          </div>
        </el-card>
      </el-col>
      <el-col class="dashboard-col" :span="12">
        <el-card class="box-card">
          <div slot="header">
            <span>存储占用</span>
          </div>
          <div class="content-box">
            <span class="content">22G / 64G</span>
            <el-icon class="iconfont icon-yingpan icon" />
          </div>
        </el-card>
      </el-col>
    </el-row>

    <el-row class="dashboard-row" :gutter="20">
      <el-col class="dashboard-col" :span="12">
        <el-card class="box-card">
          <div slot="header">
            <span>网络连接</span>
          </div>
          <div class="content-box">
            <span class="content">Njtech-Home</span>
            <el-icon class="iconfont icon-wangluo icon" />
          </div>
        </el-card>
      </el-col>
      <el-col class="dashboard-col" :span="12">
        <el-card class="box-card">
          <div slot="header">
            <span>运行时间</span>
          </div>
          <div class="content-box">
            <span class="content">10:31:04</span>
            <el-icon class="iconfont icon-shijian icon" />
          </div>
        </el-card>
      </el-col>
    </el-row>

  </div>
</template>

<script>
import { mapGetters } from 'vuex'
import '/iconfont/iconfont.css'

export default {
  name: 'Dashboard',
  computed: {
    ...mapGetters([
      'name'
    ])
  }
}
</script>

<style lang="scss" scoped>
.dashboard {
  &-container {
    margin: 30px;
  }
  &-text {
    font-size: 30px;
    line-height: 46px;
  }
}
.icon {
  font-size: 64px;
  float: right;
  margin-bottom: 10px;
}

.content {
  font-size: 40px;
  align-items: center;
}

.dashboard-row {
  margin-bottom: 20px;
}
</style>
