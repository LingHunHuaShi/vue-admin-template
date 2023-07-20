<script>
import router from '@/router'
import form from 'element-ui/packages/form'

export default {
  data() {
    return {
      installed: [ // 已经部署的算法
        {
          name: 'Yolo V5 Lite-g',
          CPU_rate: '5%',
          NPU_rate: '37%',
          run_time: '6:35:09',
          stream_number: 1
        },
        {
          name: 'Yolo V5 Lite-g',
          CPU_rate: '5%',
          NPU_rate: '37%',
          run_time: '6:35:09',
          stream_number: 1
        },
        {
          name: 'Yolo V5 Lite-g',
          CPU_rate: '5%',
          NPU_rate: '37%',
          run_time: '6:35:09',
          stream_number: 1
        }
      ],
      cloud: [ // 在云端可部署的算法
        {
          name: 'Yolo V8',
          introduction: 'Introduction for Yolo V8.Introduction for Yolo V8.Introduction for Yolo V8.Introduction for ' +
            'Yolo V8.Introduction for Yolo V8.Introduction for Yolo V8.Introduction for Yolo V8.'
        },
        {
          name: 'Yolo V8',
          introduction: 'Introduction for Yolo V8.Introduction for Yolo V8.Introduction for Yolo V8.Introduction for ' +
            'Yolo V8.Introduction for Yolo V8.Introduction for Yolo V8.Introduction for Yolo V8.'
        },
        {
          name: 'Yolo V8',
          introduction: 'Introduction for Yolo V8.Introduction for Yolo V8.Introduction for Yolo V8.Introduction for ' +
            'Yolo V8.Introduction for Yolo V8.Introduction for Yolo V8.Introduction for Yolo V8.'
        },
        {
          name: 'Yolo V8',
          introduction: 'Introduction for Yolo V8.Introduction for Yolo V8.Introduction for Yolo V8.Introduction for ' +
            'Yolo V8.Introduction for Yolo V8.Introduction for Yolo V8.Introduction for Yolo V8.'
        }
      ],
      dialogFormVisible: false,
      formLabelWidth: '120px',
      newAlgorithm: {
        VideoAddress: ''
      }
    }
  },
  computed: {
    form() {
      return form
    },
    // 计算可用的NPU核心
    usedNPUCore() {
      let totalCore = 0
      for (let i = 0; i < this.installed.length; ++i) {
        totalCore += this.installed[i].stream_number
      }
      return totalCore
    }
  },
  methods: {
    goToDetail() {
      router.push('/algorithm/detail')
    }
  }
}
</script>

<template>
  <div class="algorithm-container">
    <el-dialog title="基础配置" :visible.sync="dialogFormVisible">
      <el-form :model="newAlgorithm">
        <el-form-item label="视频流地址" :label-width="formLabelWidth">
          <el-input v-model="newAlgorithm.VideoAddress" autocomplete="off" type="url" placeholder="http://example.com" pattern="http://.*" size="30" required></el-input>
        </el-form-item>
      </el-form>
      <div slot="footer" class="dialog-footer">
        <el-button @click="dialogFormVisible = false">取消</el-button>
        <el-button type="primary" @click="dialogFormVisible = false">确定部署</el-button>
      </div>
    </el-dialog>
    <el-row class="algorithm-row">
      <el-col :span="8" class="algorithm-col">
        <el-card class="conclusion-card card" :gutter="20" type="flex">
          <div slot="header">
            <span>核心使用情况</span>
            <br>
          </div>
          <div class="content-box">
            <span style="line-height: 35px">已使用:{{ usedNPUCore }} / 3</span>
            <br>
            <div v-for="algorithm in installed" :key="algorithm" class="algorithm-text">
              {{ algorithm.name }} 使用核心数：{{ algorithm.stream_number }}
            </div>
          </div>
        </el-card>
      </el-col>
    </el-row>

    <el-row class="algorithm-row">
      <h4 class="card-title">已部署算法</h4>
      <el-col v-for="algorithm in installed" :key="algorithm" class="algorithm-col" span="8">
        <el-card class="installed-card card">
          <div slot="header">
            <span class="title">{{ algorithm.name }}</span>
          </div>
          <div class="content-box algorithm-text">
            <span>CPU占用率：{{ algorithm.CPU_rate }}</span>
            <br>
            <span>NPU占用率：{{ algorithm.NPU_rate }}</span>
            <br>
            <span>运行时间：{{ algorithm.run_time }}</span>
            <br>
            <div class="align-right">
              <el-button type="primary" class="el-button" @click="goToDetail">管理</el-button>
            </div>
          </div>
        </el-card>
      </el-col>
    </el-row>

    <el-row class="algorithm-row">
      <h4 class="card-title">云端算法</h4>
      <el-col v-for="algorithm in cloud" :key="algorithm" class="algorithm-col" span="8">
        <el-card class="cloud-card card">
          <div slot="header">
            <span class="title">{{ algorithm.name }}</span>
          </div>
          <div class="content-box algorithm-text">
            <span class="algorithm-introduction">
              {{ algorithm.introduction }}
            </span>
            <br>
            <div class="align-right">
              <el-button type="primary" class="el-button" @click="dialogFormVisible = true">点击部署</el-button>
            </div>
          </div>
        </el-card>
      </el-col>
    </el-row>
  </div>
</template>

<style scoped lang="scss">
.algorithm {
  &-container {
    margin: 30px;
  }
  &-text {
    line-height: 35px;
    font-size: 15px;
  }
  &-row {
    margin-bottom: 20px;
  }
}
.align-right {
  text-align: right;
}
.card {
  margin-right: 20px;
  margin-bottom: 20px;
}

</style>
