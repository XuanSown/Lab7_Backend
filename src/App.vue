<script setup>
import Bai1 from './components/Bai1/Bai1.vue';
import Bai2 from './components/Bai2/Bai2.vue';
import Bai3 from './components/Bai3/Bai3.vue';
import Bai4 from './components/Bai4/Bai4.vue';

import { ref } from 'vue';

const current = ref('Bai1');
const components = { Bai1, Bai2, Bai3, Bai4 };
</script>

<template>
  <select v-model="current">
    <option value="Bai1">Bài 1</option>
    <option value="Bai2">Bài 2</option>
    <option value="Bai3">Bài 3</option>
    <option value="Bai4">Bài 4</option>
  </select>
  <component :is="components[current]" />
</template>
<style scoped>
</style>
