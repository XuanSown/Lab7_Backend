<template>
    <div class="col-sm-4 m-5">
        <h2>Bình luận bài viết</h2>
        <div class="card">
            <img src="../../assets/sown.jpg" alt="Sown">
            <div class="card-body">
                <h3 class="card-title">Sown người đẹp trai top1</h3>
                <p class="card-text">Cậu là người siêng năng, chịu thương chịu khó, chăm chỉ học tập.
                 Cậu thường xuyên tập thể dục, chơi thể thao để rèn luyện cho cơ thể khỏe mạnh,
                  ngoài ra cậu còn siêng năng code, đọc tài liệu, trao dồi kiến thức bổ ích,...</p>
            </div>
        </div>
        <!-- Comment Form -->
        <form @submit.prevent="submitComment">
            <div class="mt-3">
                <textarea id="commentText" cols="60" v-model="commentText"
                placeholder="Bình luận đi nè!"></textarea>
                <p v-if="commentError" style="color: red;"> {{ commentError }}</p>
            </div>
            <button type="submit" class="btn btn-success">Gửi</button>
        </form>
        <!-- Comment List -->
        <div class="mt-3" v-if="comments.lenght">
            <h5>Danh sách bình luận:</h5>
            <ul style="list-style-type: circle;">
                <li v-for="(comment, index) in comments" :key="index">
                    <p><strong>{{ comment.name }}</strong>: {{ comment.text }}</p>
                </li>
            </ul>
        </div>
    </div>
</template>

<script setup>
import { ref } from 'vue';

const commentText = ref('');
const comments = ref([]);
const commentError = ref('');

//Nhận props từ component cha
const props = defineProps(['username']);

function submitComment(){
    commentError.value = '';

    if(!commentText.value.trim()) {
        commentError.value = 'Vui lòng nhập bình luận trước khi gửi.';
    } else {
        comments.value.push({
            name: props.username,
            text: commentText.value.trim()
        });
        //Xóa dữ liệu khi gửi thành công
        commentText.value = '';
    }
}
</script>