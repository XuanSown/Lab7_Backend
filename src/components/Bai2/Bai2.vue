<template>
    <div class="p-5 col-sm-4" v-if="!isLoggedIn">
        <h3>Form đăng nhập</h3>
        <form @submit.prevent="login">
            <div class="mb-3 mt-3">
                <label>Email:</label>
                <input type="email" class="form-control" v-model="email" placeholder="Nhập email">
                <p v-if="emailError" style="color: red;">{{ emailError }}</p>
            </div>
            <div class="mb-3">
                <label>Mật khẩu:</label>
                <input type="password" class="form-control" v-model="password" placeholder="Nhập password">
                <p v-if="passwordError" style="color: red;">{{ passwordError }}</p>
            </div>
            <button type="submit" class="btn btn-primary">Đăng nhập</button>
        </form>
    </div>

    <!-- Người dùng sau khi đăng nhập -->
     <div class="p-5 col-sm-5">
        <h3>Chào mừng, {{ email }}</h3>
        <button @click="logout" class="btn btn-primary">Đăng xuất</button>
     </div>
</template>

<script setup>
import { ref } from 'vue';

const email = ref('');
const password = ref('');
const isLoggedIn = ref(false);
const emailError = ref('');
const passwordError = ref('');

const emailPattern = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;


//Login
const login = () => {
    // Reset lỗi
    emailError.value = '';
    passwordError.value = '';

    if (!email.value) {
        emailError.value = 'Vui lòng nhập email.';
    } else if(!emailPattern.test(email.value)) {
        emailError.value = 'Email không hợp lệ.';
    }

    if(!password.value) {
        passwordError.value = 'Vui lòng nhập mật khẩu.';
    }

    if(!emailError.value && !passwordError.value) {
        isLoggedIn.value = true;
    }
}


//Logout
const logout = () => {
    isLoggedIn.value = false;
    email.value = '';
    password.value = '';
    emailError.value = '';
    passwordError.value = '';
}
</script>