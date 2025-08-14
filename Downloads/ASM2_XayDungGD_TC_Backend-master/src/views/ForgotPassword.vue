<template>
  <div class="container mt-5">
    <h2>🔑 Quên mật khẩu</h2>
    <form @submit.prevent="resetPassword" class="mt-3">
      <input v-model="email" placeholder="Nhập email của bạn" class="form-control mb-3" />
      <button class="btn btn-warning w-100">Lấy lại mật khẩu</button>
    </form>
  </div>
</template>

<script setup>
import { ref } from 'vue'

const email = ref('')

const resetPassword = () => {
  if (email.value) {
    const users = JSON.parse(localStorage.getItem('users') || '[]')
    const user = users.find(u => u.email === email.value)
    if (user) {
      alert('Mật khẩu của bạn là: ' + user.password)
    } else {
      alert('Không tìm thấy email này!')
    }
  } else {
    alert('Vui lòng nhập email')
  }
}
</script>
