<template>
    <div class="flex flex-col gap-4 mb-4">
      <div class="flex space-x-4">
        <select v-model="filterColumn" @change="applyFilter" class="p-2 border-2 border-[#1f2937a] rounded">
          <option value="">Pilih Kolom</option>
          <option value="nama">Nama</option>
          <option value="email">Email</option>
          <option value="umur">Umur</option>
        </select>
        <input v-model="searchQuery" placeholder="Search..." @input="applyFilter" class="p-2 border-2 border-[#1f2937a] rounded" />
      </div>
      <div>
        <select v-model="statusFilter" @change="applyFilter" class="p-2 border-2 border-[#1f2937a] rounded">
          <option value="">Semua Status</option>
          <option value="Aktif">Aktif</option>
          <option value="Tidak Aktif">Tidak Aktif</option>
        </select>
      </div>
      <div class="flex space-x-4">
        <select v-model="sortColumn" @change="applySort" class="p-2 border-2 border-[#1f2937a] rounded">
          <option value="">Urutkan Kolom</option>
          <option value="nama">Nama</option>
          <option value="email">Email</option>
          <option value="umur">Umur</option>
        </select>
        <select v-model="sortDirection" @change="applySort" class="p-2 border-2 border-[#1f2937a] rounded">
          <option value="true">ASC</option>
          <option value="false">DESC</option>
        </select>
      </div>
    </div>
  </template>
  
  <script setup>
  import { ref } from 'vue';
  
  const emit = defineEmits(['applyFilter', 'applySort']);
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
  