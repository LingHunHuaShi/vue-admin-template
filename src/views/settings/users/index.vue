<template>
  <div class="app-container">
    <!-- Add a table to display all users -->
    <el-table :data="users" style="width: 100%" stripe>
      <el-table-column prop="ID" label="ID"></el-table-column>
      <el-table-column prop="username" label="用户名"></el-table-column>
      <el-table-column prop="password" label="密码">
        <template slot-scope="scope">
          <el-input v-model="scope.row.password" size="small"/>
        </template>
      </el-table-column>
      <el-table-column prop="level" label="等级"></el-table-column>
      <el-table-column prop="registrationDate" label="注册日期"></el-table-column>
      <el-table-column label="Actions">
        <template slot-scope="scope">
          <!-- Add buttons to change password and delete user -->
          <el-button type="primary" size="mini" @click="updatePassword(scope.row)">
            更新密码
          </el-button>
          <el-button type="danger" size="mini" @click="deleteUser(scope.row)">
            删除用户
          </el-button>
        </template>
      </el-table-column>
    </el-table>

    <!-- Add a button to commit changes -->
    <el-button type="primary" @click="onSubmit">提交更改</el-button>
    <el-button @click="onCancel">取消更改</el-button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      users: [
        {
          ID: 1,
          username: 'john_doe',
          password: 'secretpassword',
          level: '超级管理员',
          registrationDate: '2023-07-23 13:30:29'
        },
        {
          ID: 2,
          username: 'alice_smith',
          password: 'alicepassword',
          level: '普通管理员',
          registrationDate: '2023-07-22 15:37:23'
        },
        {
          ID: 3,
          username: 'bob_johnson',
          password: 'bobpassword',
          level: '普通用户',
          registrationDate: '2023-07-21 01:24:33'
        }
        // Add more users as needed
      ],
      form: {
        // ... Form data as before ...
      }
    }
  },
  methods: {
    // ... Methods as before ...
  },
  mounted() {
    // ... Fetch users or perform any other actions on mount ...
  }
}
</script>

<style scoped>
.line {
  text-align: center;
}
</style>
