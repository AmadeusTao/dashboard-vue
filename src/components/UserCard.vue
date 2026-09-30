<script setup>
import { ref } from 'vue'

defineProps({
  name: String,
  email: String,
  phone: String,
  company: String,
  city: String
})

const tampilDetail = ref(false)

function toggleDetail() {
  tampilDetail.value = !tampilDetail.value
}
</script>

<template>
  <div class="user-card">
    <h3>{{ name }}</h3>
    <p>{{ email }}</p>

    <button @click="toggleDetail">
      {{ tampilDetail ? 'Sembunyikan' : 'Lihat Detail' }}
    </button>

    <div v-if="tampilDetail" class="detail">
      <p>Telepon: {{ phone }}</p>
      <p>Perusahaan: {{ company }}</p>
      <p>Kota: {{ city }}</p>
    </div>
  </div>
</template>

<style scoped>
.user-card {
  padding: 16px;
  margin-bottom: 12px;
  border: 1px solid #ddd;
  border-radius: 8px;
}

.user-card button {
  padding: 6px 10px;
  margin-top: 8px;
  cursor: pointer;
}

.detail {
  margin-top: 12px;
  padding: 10px;
  background-color: #f5f5f5;
  border-radius: 6px;
}
</style>