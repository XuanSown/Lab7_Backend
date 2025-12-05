<template>
    <div class="p-5 col-sm-4" v-if="!isRegister">
        <h3>Form đăng ký</h3>
        <form @submit.prevent="register">
            <div class="mb-3 mt-3">
                <label>Họ tên:</label>
                <input type="text" class="form-control" v-model="name" placeholder="Nhập tên">
                <p v-if="nameError" style="color: red;">{{ nameError }}</p>
            </div>
            <div class="mb-3">
                <label>Email:</label>
                <input type="email" class="form-control" v-model="email" placeholder="Nhập email">
                <p v-if="emailError" style="color: red;">{{ emailError }}</p>
            </div>
            <div class="mb-3">
                <label>Mật khẩu:</label>
                <input type="password" class="form-control" v-model="password" placeholder="Nhập password">
                <p v-if="passwordError" style="color: red;">{{ passwordError }}</p>
            </div>
            <div class="mb-3">
                <label>Ngày sinh</label>
                <input type="date" class="form-control" v-model="dob">
                <p v-if="dobError" style="color: red;">{{ dobError }}</p>
            </div>
            <div class="mb-3">
                <label>Giới tính</label>
                <select class="form-control" v-model="gender">
                    <option value="Nam">Nam</option>
                    <option value="Nữ">Nữ</option>
                    <option value="Khác">Khác</option>
                </select>
                <p v-if="genderError" style="color: red;">{{ genderError }}</p>
            </div>
            <div class="mb-3">
                <label>Ngôn ngữ</label>
                <select class="form-control" v-model="language">
                    <option value="Tiếng Việt">Tiếng Việt</option>
                    <option value="English">English</option>
                    <option value="Tiếng Nhật">Tiếng Nhật</option>
                </select>
                <p v-if="languageError" style="color: red;">{{ languageError }}</p>
            </div>
            <button type="submit" class="btn btn-primary">Đăng ký</button>
        </form>
    </div>

    <!-- Hiển thị thông tin người dùng sau khi đăng ký -->
        <div class="p-5 col-sm-5" v-else>
            <h3>Thông tin đăng ký</h3>
            <p><strong>Họ tên: </strong> {{ name }}</p>
            <p><strong>Email: </strong> {{ email }}</p>
            <p><strong>Ngày sinh: </strong> {{ dob }}</p>
            <p><strong>Giới tính: </strong> {{ gender }}</p>
            <p><strong>Ngôn ngữ: </strong> {{ language }}</p>
            <button @click="toPage" class="btn btn-primary">Quay lại trang đăng ký</button>
        </div> 
</template>

<script setup>
import { ref } from 'vue';
const name = ref('');
const email = ref('');
const password = ref('');
const dob = ref('');
const gender = ref('Nam');
const language = ref('Tiếng Việt');

const isRegister = ref(false);
const emailPattern = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;

const nameError = ref('');
const emailError = ref('');
const passwordError = ref('');
const dobError = ref('');
const genderError = ref('');
const languageError = ref('');

//Register
const register = () => {
    // Reset lỗi
    nameError.value = '';
    emailError.value = '';
    passwordError.value = '';
    dobError.value = '';
    genderError.value = '';
    languageError.value = '';

    if(!name.value) {
        nameError.value = 'Vui lòng nhập họ tên.';
    }

    if(!email.value) {
        emailError.value= 'Vui lòng nhập email.';
    } else if(!emailPattern.test(email.value)) {
        emailError.value = 'Email không hợp lệ.';
    }

    if(!password.value) {
        passwordError.value = 'Vui lòng nhập mật khẩu.';
    }

    if(!dob.value) {
        dobError.value = 'Vui lòng chọn ngày sinh.';
    }

    if(!gender.value) {
        genderError.value = 'Vui lòng chọn giới tính.';
    }

    if(!language.value) {
        languageError.value = 'Vui lòng chọn ngôn ngữ.';
    }

    if(!nameError.value && !emailError.value && !passwordError.value && !dobError.value && !genderError.value && !languageError.value) {
        isRegister.value = true;
    }
}

//Quay lại trang đăng ký
const toPage = () => {
    isRegister.value = false;
    name.value = '';
    email.value = '';
    password.value = '';
    dob.value = '';
}

</script>