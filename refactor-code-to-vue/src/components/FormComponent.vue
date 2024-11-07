<template>
    <form @submit.prevent="handleSubmit" class="mb-4">
      <div class="flex space-x-4">
        <input type="text" v-model="user.nama" placeholder="Nama" required class="p-2 border-2 border-[#1f2937a] rounded" />
        <input type="email" v-model="user.email" placeholder="Email" required class="p-2 border-2 border-[#1f2937a] rounded" />
        <input type="number" v-model.number="user.umur" placeholder="Umur" min="1" required class="p-2 border-2 border-[#1f2937a] rounded" />
        <select v-model="user.status" required class="p-2 border-2 border-[#1f2937a] rounded">
          <option value="">Status</option>
          <option value="Aktif">Aktif</option>
          <option value="Tidak Aktif">Tidak Aktif</option>
        </select>
        <button type="submit" class="bg-[#1f2937] text-white px-4 py-2 rounded">{{ userToEdit ? 'Update' : 'Add' }}</button>
      </div>
    </form>
  </template>
  
  <script setup>
  import { ref, watch } from 'vue';
  
  const emit = defineEmits(['updateUser', 'adduser'])
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
  