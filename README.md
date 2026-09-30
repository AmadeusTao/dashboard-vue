# Technical Assignment 2

Component-Based UI with Vue.js 3 Composition API.

## Fitur

### 1. Detail Toggle
Setiap user memiliki tombol **Lihat Detail** untuk menampilkan informasi tambahan berupa:

- Telepon
- Perusahaan
- Kota

State detail disimpan secara lokal pada komponen `UserCard.vue`.

### 2. Pencarian User
User dapat dicari berdasarkan nama melalui kolom pencarian.

### 3. Sorting User
Daftar user dapat diurutkan berdasarkan nama:

- A-Z
- Z-A

Sorting dilakukan menggunakan chained computed dari hasil pencarian user.

## Menjalankan Project

```bash
npm install
npm run dev