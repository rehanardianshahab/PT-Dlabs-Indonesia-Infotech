<template>
    <form @submit.prevent="handleSubmit">
      <input type="text" v-model="user.nama" placeholder="Nama" required />
      <input type="email" v-model="user.email" placeholder="Email" required />
      <input type="number" v-model.number="user.umur" placeholder="Umur" min="1" required />
      <select v-model="user.status" required>
        <option value="">Status</option>
        <option value="Aktif">Aktif</option>
        <option value="Tidak Aktif">Tidak Aktif</option>
      </select>
      <button type="submit" class="bg-blue-500 text-white px-4 py-2">{{ userToEdit ? 'Update' : 'Add' }}</button>
    </form>
  </template>
  
  <script setup>
  import { ref, watch, computed } from 'vue';
  import { emit } from 'vue';
  
  const props = defineProps(['userToEdit']);
  const user = ref({
    nama: '',
    email: '',
    umur: null,
    status: '',
  });
  
  watch(
    () => props.userToEdit,
    (newUser) => {
      if (newUser) {
        user.value = { ...newUser };
      }
    }
  );
  
  const handleSubmit = () => {
    if (props.userToEdit) {
      emit('updateUser', user.value, props.userToEdit.index);
    } else {
      emit('addUser', user.value);
    }
    resetForm();
  };
  
  const resetForm = () => {
    user.value = { nama: '', email: '', umur: null, status: '' };
  };
  </script>
  