<template>
  <div class="admin-list">
    <h2>🛡️ Danh sách quản trị viên</h2>
    <table>
      <thead>
        <tr>
          <th>Họ và Tên</th>
          <th>Email</th>
          <th>Số điện thoại</th>
          <th>Giới tính</th>
          <th>Vai trò</th>
          <th>Mật khẩu</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="admin in admins" :key="admin.id">
          <td>{{ admin.name }}</td>
          <td>{{ admin.email }}</td>
          <td>{{ admin.phone }}</td>
          <td>{{ admin.gender }}</td>
          <td>{{ admin.role }}</td>
          <td>{{ maskPassword(admin.password) }}</td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
export default {
  name: 'AdminList',
  data() {
    return {
      admins: []
    }
  },
  mounted() {
    const admins = JSON.parse(localStorage.getItem('admins') || '[]')
    this.admins = admins
  },
  methods: {
    maskPassword(password) {
      return '*'.repeat(password.length)
    },
  },
}
</script>

<style scoped>
.admin-list {
  padding: 20px;
}
table {
  width: 100%;
  border-collapse: collapse;
}
th, td {
  padding: 8px;
  border: 1px solid #ccc;
  text-align: left;
}
</style>
