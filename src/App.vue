<script setup>
import { ref, computed, onMounted } from 'vue'
import UserCard from './components/UserCard.vue'

const users = ref([])
const loading = ref(false)
const error = ref(null)
const queryPencarian = ref('')
const arahUrutan = ref('asc')

const penggunaTersaring = computed(() => {
  const keyword = queryPencarian.value.toLowerCase()

  return users.value.filter((user) => {
    return user.name.toLowerCase().includes(keyword)
  })
})

const penggunaDiurutkan = computed(() => {
  const hasil = [...penggunaTersaring.value]

  return hasil.sort((a, b) => {
    if (arahUrutan.value === 'asc') {
      return a.name.localeCompare(b.name)
    }

    return b.name.localeCompare(a.name)
  })
})

async function ambilPengguna() {
  loading.value = true
  error.value = null

  try {
    const response = await fetch(
      'https://jsonplaceholder.typicode.com/users'
    )

    if (!response.ok) {
      throw new Error('Gagal mengambil data pengguna')
    }

    users.value = await response.json()
  } catch (err) {
    error.value = err.message
  } finally {
    loading.value = false
  }
}

onMounted(() => {
  ambilPengguna()
})
</script>

<template>
  <main class="container">
    <h1>Dashboard Vue</h1>

    <div class="controls">
      <button @click="ambilPengguna">
        Muat Pengguna
      </button>

      <input
        v-model="queryPencarian"
        type="text"
        placeholder="Cari pengguna..."
      >

      <button
        :class="{ aktif: arahUrutan === 'asc' }"
        @click="arahUrutan = 'asc'"
      >
        Urutkan A-Z
      </button>

      <button
        :class="{ aktif: arahUrutan === 'desc' }"
        @click="arahUrutan = 'desc'"
      >
        Urutkan Z-A
      </button>
    </div>

    <p v-if="loading">
      Sedang mengambil data...
    </p>

    <p v-else-if="error">
      {{ error }}
    </p>

    <p v-else-if="penggunaDiurutkan.length === 0">
      Data pengguna tidak tersedia.
    </p>

    <div v-else>
      <UserCard
        v-for="user in penggunaDiurutkan"
        :key="user.id"
        :name="user.name"
        :email="user.email"
        :phone="user.phone"
        :company="user.company.name"
        :city="user.address.city"
      />
    </div>
  </main>
</template>

<style scoped>
.container {
  max-width: 800px;
  margin: 40px auto;
  font-family: Arial, sans-serif;
}

.controls {
  display: flex;
  gap: 10px;
  margin-bottom: 20px;
}

button {
  padding: 8px 12px;
  cursor: pointer;
}

input {
  padding: 8px 12px;
}

button.aktif {
  background-color: #176b87;
  color: white;
}
</style>