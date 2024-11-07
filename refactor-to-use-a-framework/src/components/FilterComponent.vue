<template>
    <div class="flex flex-wrap gap-4">
      <select v-model="filterColumn" @change="applyFilter">
        <option value="">Pilih Kolom</option>
        <option value="nama">Nama</option>
        <option value="email">Email</option>
        <option value="umur">Umur</option>
      </select>
      <input v-model="searchQuery" placeholder="Search..." @input="applyFilter" />
      <select v-model="statusFilter" @change="applyFilter">
        <option value="">Semua Status</option>
        <option value="Aktif">Aktif</option>
        <option value="Tidak Aktif">Tidak Aktif</option>
      </select>
      <select v-model="sortColumn" @change="applySort">
        <option value="">Urutkan Kolom</option>
        <option value="nama">Nama</option>
        <option value="email">Email</option>
        <option value="umur">Umur</option>
      </select>
      <select v-model="sortDirection" @change="applySort">
        <option value="true">ASC</option>
        <option value="false">DESC</option>
      </select>
    </div>
  </template>
  
  <script setup>
  import { ref } from 'vue';
  
  const filterColumn = ref('');
  const searchQuery = ref('');
  const statusFilter = ref('');
  const sortColumn = ref('');
  const sortDirection = ref(true);
  
  const applyFilter = () => {
    emit('applyFilter', { filterColumn, searchQuery, statusFilter });
  };
  
  const applySort = () => {
    emit('applySort', { sortColumn, sortDirection });
  };
  </script>
  