<template>
  <table class="w-full table-auto border-collapse shadow-lg rounded-lg overflow-hidden">
    <thead>
      <tr class="bg-gray-800 text-white">
        <th class="px-6 py-4 text-left font-semibold">Nama</th>
        <th class="px-6 py-4 text-left font-semibold">Email</th>
        <th class="px-6 py-4 text-center font-semibold">Umur</th>
        <th class="px-6 py-4 text-center font-semibold">Status</th>
        <th class="px-6 py-4 text-center font-semibold">Actions</th>
      </tr>
    </thead>
    <tbody>
      <tr
        v-for="(user, index) in filteredData"
        :key="index"
        class="bg-white hover:bg-gray-100 transition-colors duration-200 border-b"
      >
        <td class="px-6 py-4 text-gray-800">{{ user.nama }}</td>
        <td class="px-6 py-4 text-gray-800">{{ user.email }}</td>
        <td class="px-6 py-4 text-center text-gray-800">{{ user.umur }}</td>
        <td class="px-6 py-4">
          <div
            class="mx-auto text-center w-[140px] rounded font-semibold py-2 text-sm"
            :class="user.status === 'Aktif' ? 'text-green-500 bg-green-200' : 'text-red-500 bg-red-200'"
          >
            {{ user.status }}
          </div>
        </td>
        <td class="px-6 py-4 flex items-center justify-center space-x-2">
          <button
            @click="$emit('editUser', user, index)"
            class="bg-blue-500 hover:bg-blue-600 text-white px-4 py-2 rounded-lg shadow-md transition-colors duration-150"
          >
            Edit
          </button>
          <button
            @click="$emit('deleteUser', index)"
            class="bg-red-500 hover:bg-red-600 text-white px-4 py-2 rounded-lg shadow-md transition-colors duration-150"
          >
            Delete
          </button>
        </td>
      </tr>
    </tbody>
  </table>
</template>

<script setup>
defineProps(['filteredData']);
</script>
