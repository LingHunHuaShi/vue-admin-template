<template>
  <div class="cases">
    <h2 class="page-title">案例列表</h2>

    <!-- Search input field -->
    <el-input
        v-model="searchQuery"
        placeholder="请输入关键词进行搜索"
        clearable
        @input="performSearch"
    />

    <el-table :data="filteredCases" style="width: 100%">
      <el-table-column prop="caseID" label="案例ID" width="100"/>
      <el-table-column prop="userID" label="用户ID" width="100"/>
      <el-table-column prop="title" label="案例标题"/>
      <el-table-column prop="description" label="案例描述"/>
      <el-table-column prop="status" label="状态" width="100"/>
      <el-table-column prop="submissionDate" label="提交日期" width="150"/>
      <el-table-column prop="compeletionDate" label="完成日期" width="150"/>
      <el-table-column prop="solution" label="解决方案"/>
      <el-table-column prop="severity" label="严重等级" width="100"/>
      <el-table-column label="操作" width="120">
        <template slot-scope="scope">
          <el-button v-if="!scope.row.compeletionDate" type="primary" @click="archiveCase(scope.row)">
            归档
          </el-button>
          <el-button v-else type="success" @click="writeSolution(scope.row)">
            查看解决方案
          </el-button>
        </template>
      </el-table-column>
    </el-table>

    <!-- Solution Dialog -->
    <el-dialog title="解决方案" :visible.sync="solutionDialogVisible">
      <el-form :model="solutionForm" label-width="100px">
        <el-form-item label="解决方案">
          <el-input v-model="solutionForm.solution" type="textarea" :rows="6" placeholder="请输入解决方案"/>
        </el-form-item>
      </el-form>
      <div slot="footer">
        <el-button @click="solutionDialogVisible = false">取消</el-button>
        <el-button type="primary" :loading="savingSolution" @click="saveSolution">保存</el-button>
      </div>
    </el-dialog>
  </div>
</template>

<script>
export default {
  data() {
    return {
      cases: [
        // Sample cases data, replace with actual data from the database
        {
          caseID: 1,
          userID: 101,
          title: 'Login Issue',
          description: 'Unable to log in to the system.',
          status: 'Open',
          submissionDate: '2023-07-15',
          compeletionDate: null,
          solution: '',
          severity: 'High'
        },
        {
          caseID: 2,
          userID: 102,
          title: 'File Not Found',
          description: 'Cannot locate the required file.',
          status: 'Open',
          submissionDate: '2023-07-17',
          compeletionDate: null,
          solution: '',
          severity: 'Medium'
        },
        {
          caseID: 3,
          userID: 103,
          title: 'Application Crash',
          description: 'Application crashes on startup.',
          status: 'Closed',
          submissionDate: '2023-07-18',
          compeletionDate: '2023-07-20',
          solution: 'Reinstalled the application, issue resolved.',
          severity: 'Low'
        }
        // Add more test cases here...
      ],
      searchQuery: '',
      solutionDialogVisible: false,
      solutionForm: {
        caseID: null,
        solution: ''
      },
      savingSolution: false
    }
  },
  computed: {
    // Filter the cases based on the search query
    // eslint-disable-next-line vue/no-dupe-keys
    filteredCases() {
      if (this.searchQuery.trim() === '') {
        // If the search query is empty, show all cases
        return this.cases
      } else {
        // If the search query is not empty, filter the cases based on the query
        const query = this.searchQuery.trim().toLowerCase()
        return this.cases.filter(
            (c) =>
                c.title.toLowerCase().includes(query) || // Search by title
                c.description.toLowerCase().includes(query) || // Search by description
                c.severity.toLowerCase().includes(query) || // Search by severity
                c.status.toLowerCase().includes(query) || // Search by status
                c.userID.toString().includes(query) || // Search by userID (assuming userID is a number)
                c.caseID.toString().includes(query) // Search by caseID (assuming caseID is a number)
        )
      }
    }
  },
  methods: {
    archiveCase(row) {
      if (!row.compeletionDate) {
        // Display the solution dialog
        this.solutionForm.caseID = row.caseID
        this.solutionForm.solution = row.solution
        this.solutionDialogVisible = true
      }
    },
    writeSolution(row) {
      // Display the solution dialog to view the solution
      this.solutionForm.caseID = row.caseID
      this.solutionForm.solution = row.solution
      this.solutionDialogVisible = true
    },
    saveSolution() {
      // Here you can save the solution to the database
      // For demonstration purposes, we'll update the case data in the cases array
      this.savingSolution = true

      // Simulating an API call to save the solution to the database
      setTimeout(() => {
        const caseToUpdate = this.cases.find((c) => c.caseID === this.solutionForm.caseID)
        if (caseToUpdate) {
          caseToUpdate.solution = this.solutionForm.solution
          caseToUpdate.compeletionDate = new Date().toISOString().split('T')[0]
          this.$message.success('解决方案已保存，并已归档该案例。')
          this.solutionDialogVisible = false
        } else {
          this.$message.error('保存失败，未找到相关案例。')
        }
        this.savingSolution = false
      }, 1500)
    },
    // ... The rest of the methods as before ...

    // Perform search when the user enters a search query
    performSearch() {
      // The search will automatically update the table because of the computed property
    }
  }
}
</script>

<style scoped>
/* Add any custom styles for the page here */
.cases {
  max-width: 1200px;
  margin: 0 auto;
  padding: 20px;
}

.page-title {
  text-align: center;
  font-size: 24px;
  margin-bottom: 20px;
}
</style>
