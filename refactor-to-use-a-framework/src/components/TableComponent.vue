<template>
    <table class="w-full border-collapse">
      <thead>
        <tr>
          <th>Nama</th>
          <th>Email</th>
          <th>Umur</th>
          <th>Status</th>
          <th>Actions</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(user, index) in filteredData" :key="index">
          <td>{{ user.nama }}</td>
          <td>{{ user.email }}</td>
          <td>{{ user.umur }}</td>
          <td>{{ user.status }}</td>
          <td>
            <button @click="$emit('editUser', user, index)">Edit</button>
            <button @click="$emit('deleteUser', index)">Delete</button>
          </td>
        </tr>
      </tbody>
    </table>
  </template>
  
  <script setup>
  defineProps(['filteredData']);
  </script>
  