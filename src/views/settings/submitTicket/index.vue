<template>
  <div class="page-center">
    <div class="cases">
      <h2 class="form-title">工单提交系统</h2>
      <el-form ref="form" :model="form" label-width="120px">
        <el-form-item label="案例标题">
          <el-input v-model="form.title" placeholder="请输入案例标题"/>
        </el-form-item>
        <el-form-item label="案例描述">
          <el-input
              v-model="form.description"
              type="textarea"
              :rows="4"
              placeholder="请输入问题的描述"
          />
        </el-form-item>
        <el-form-item label="严重等级">
          <el-select v-model="form.severity" placeholder="请选择严重等级">
            <el-option label="轻度" value="0"/>
            <el-option label="中等" value="1"/>
            <el-option label="严重" value="2"/>
            <el-option label="非常严重" value="3"/>
          </el-select>
        </el-form-item>
        <el-form-item>
          <el-button type="primary" @click="onSubmit">提交</el-button>
          <el-button @click="onCancel">取消</el-button>
        </el-form-item>
      </el-form>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      form: {
        title: '',
        description: '',
        severity: '' // Default severity value, you can change this if needed
      }
    }
  },
  methods: {
    // ... The rest of the methods as before ...
  }
}
</script>

<style>
/* Add any custom styles for the form here */
.page-center {
  display: flex;
  justify-content: center;
  align-items: center;
  min-height: 80vh;
}

.cases {
  max-width: 600px;
  padding: 20px;
  border: 1px solid #ccc;
  border-radius: 8px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

.form-title {
  text-align: center;
  font-size: 24px;
  margin-bottom: 20px;
}

.el-form-item__label {
  font-weight: bold;
}

.el-input,
.el-select {
  width: 100%;
}

.el-textarea {
  width: 100%;
}

.el-button {
  margin-right: 10px;
}

.el-button--primary {
  background-color: #007bff;
  border-color: #007bff;
}

.el-button--primary:hover {
  background-color: #0056b3;
  border-color: #0056b3;
}

.el-button--primary:active {
  background-color: #004080;
  border-color: #004080;
}

.el-button--primary:focus {
  box-shadow: 0 0 0 3px rgba(0, 123, 255, 0.2);
}

.el-button--success {
  background-color: #28a745;
  border-color: #28a745;
}

.el-button--success:hover {
  background-color: #1b872d;
  border-color: #1b872d;
}

.el-button--success:active {
  background-color: #0e4a1a;
  border-color: #0e4a1a;
}

.el-button--success:focus {
  box-shadow: 0 0 0 3px rgba(40, 167, 69, 0.2);
}

.el-button--danger {
  background-color: #dc3545;
  border-color: #dc3545;
}

.el-button--danger:hover {
  background-color: #a71f31;
  border-color: #a71f31;
}

.el-button--danger:active {
  background-color: #590a13;
  border-color: #590a13;
}

.el-button--danger:focus {
  box-shadow: 0 0 0 3px rgba(220, 53, 69, 0.2);
}
</style>
