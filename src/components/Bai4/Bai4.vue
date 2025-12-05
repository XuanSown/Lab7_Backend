<template>
    <!-- Nếu người dùng chưa đăng nhập, hiện thị form đăng nhập -->
     <LoginComponent v-if="!isLoggedIn" @loggedIn="handleLoginSuccess"/>

     <!-- Nếu người dùng đã đăng nhập, hiện thị component bình luận -->
      <CommentComponent v-else :username="loggedInUser"/>
</template>

<script setup>
import { ref } from 'vue';
import LoginComponent from './LoginComponent.vue';
import CommentComponent from './CommentComponent.vue';


const isLoggedIn = ref(false);
const loggedInUser = ref('');

//Xử lý khi đăng nhập thành công
function handleLoginSuccess(username) {
    isLoggedIn.value = true;
    loggedInUser.value = username;
}
</script>