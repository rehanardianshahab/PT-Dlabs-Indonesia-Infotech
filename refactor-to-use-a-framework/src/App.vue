<template>
  <div class="app">
    <Header />
    <main class="container mx-auto">
      <FormComponent @addUser="addUser" :userToEdit="userToEdit" @updateUser="updateUser" />
      <FilterComponent :applyFilter="applyFilter" :applySort="applySort" />
      <TableComponent
        :filteredData="filteredData"
        @editUser="prepareEditUser"
        @deleteUser="deleteUser"
      />
    </main>
    <Footer />
  </div>
</template>

<script setup>
import { ref } from 'vue';
import Header from './components/Header.vue';
import Footer from './components/Footer.vue';
import FormComponent from './components/FormComponent.vue';
import TableComponent from './components/TableComponent.vue';
import FilterComponent from './components/FilterComponent.vue';

const data = ref(JSON.parse(localStorage.getItem('userData')) || []);
const userToEdit = ref(null);

const addUser = (user) => {
  data.value.push(user);
  localStorage.setItem('userData', JSON.stringify(data.value));
};

const updateUser = (updatedUser, index) => {
  data.value[index] = updatedUser;
  localStorage.setItem('userData', JSON.stringify(data.value));
  userToEdit.value = null;
};

const deleteUser = (index) => {
  data.value.splice(index, 1);
  localStorage.setItem('userData', JSON.stringify(data.value));
};

const applyFilter = (filteredResults) => {
  filteredData.value = filteredResults;
};

const applySort = (sortedResults) => {
  filteredData.value = sortedResults;
};

const prepareEditUser = (user, index) => {
  userToEdit.value = { ...user, index };
};

const filteredData = ref(data.value);
</script>
