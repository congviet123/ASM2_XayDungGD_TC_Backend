<template>
  <div class="container mt-5">
    <h2>📝 Đăng ký tài khoản</h2>
    <form @submit.prevent="register" class="mt-3">
      <input v-model="name" placeholder="Họ tên" class="form-control mb-3" />
      <input v-model="email" placeholder="Email" class="form-control mb-3" />
      <input v-model="username" placeholder="Tên đăng nhập" class="form-control mb-3" />
      <input type="password" v-model="password" placeholder="Mật khẩu" class="form-control mb-3" />
      <select v-model="role" class="form-control mb-3">
        <option value="user">User</option>
        <option value="admin">Admin</option>
      </select>
      <button class="btn btn-success w-100">Đăng ký</button>
    </form>
  </div>
</template>

<script setup>
import { ref } from 'vue'
import { useRouter } from 'vue-router'

const name = ref('')
const email = ref('')
const username = ref('')
const password = ref('')
const role = ref('user')
const router = useRouter()

const register = () => {
  if (name.value && email.value && username.value && password.value) {
    const userData = { name: name.value, email: email.value, username: username.value, password: password.value, role: role.value };
    if (role.value === 'admin') {
      const admins = JSON.parse(localStorage.getItem('admins') || '[]');
      admins.push(userData);
      localStorage.setItem('admins', JSON.stringify(admins));
    } else {
      const users = JSON.parse(localStorage.getItem('users') || '[]');
      users.push(userData);
      localStorage.setItem('users', JSON.stringify(users));
    }
    alert('Đăng ký thành công!');
    router.push({ name: 'Login' });
  } else {
    alert('Vui lòng nhập đầy đủ thông tin');
  }
}
</script>
