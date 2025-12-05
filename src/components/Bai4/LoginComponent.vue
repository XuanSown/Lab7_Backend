<template>
    <div class="p-5 col-sm-4">
        <h3>Đăng nhập</h3>
        <form @submit.prevent="handleLogin">
            <div class="mb-3 mt-3">
                <label for="username">Tên đăng nhập:</label>
                <input type="text" class="form-control" id="username" v-model="username"
                    placeholder="Nhập tên đăng nhập">
                <p v-if="usernameError" style="color: red;">{{ usernameError }}</p>
            </div>
            <div class="mb-3">
                <label for="password">Mật khẩu:</label>
                <input type="password" class="form-control" id="password" v-model="password"
                    placeholder="Nhập password">
                <p v-if="passwordError" style="color: red;">{{ passwordError }}</p>
            </div>
            <button type="submit" class="btn btn-primary">Đăng nhập</button>
        </form>
    </div>
</template>

<script setup>
import { ref } from 'vue';

const username = ref('');
const password = ref('');
const usernameError = ref('');
const passwordError = ref('');

//Login
const emit = defineEmits(['loggedIn']);
function handleLogin() {
    //Reset lỗi
    usernameError.value = '';
    passwordError.value = '';

    if (!username.value) {
        usernameError.value = 'Vui lòng nhập tên đăng nhập.';
    }
    if (!password.value) {
        passwordError.value = 'Vui lòng nhập mật khẩu.';
    }
    if (!usernameError.value && !passwordError.value) {
        // Phát sự kiện đăng nhập thành công
        emit('loggedIn', username.value);
    }
}
</script>