<template>
  <div class="app">
    <Header />
    <main class="mx-auto">
      {{ filterCriteria }}
      <div class="m-8 sm:m-10">
        <FormComponent @addUser="addUser" :userToEdit="userToEdit" @updateUser="updateUser" />
        <FilterComponent @applyFilter="applyFilter" @applySort="applySort" />
        <TableComponent
          :filteredData="filteredData"
          @editUser="prepareEditUser"
          @deleteUser="deleteUser"
        />
      </div>
    </main>
    <Footer />
  </div>
</template>

<script setup>
import { ref, computed } from 'vue';
import Header from './components/Header.vue';
import Footer from './components/Footer.vue';
import FormComponent from './components/FormComponent.vue';
import TableComponent from './components/TableComponent.vue';
import FilterComponent from './components/FilterComponent.vue';

const data = ref(JSON.parse(localStorage.getItem('userData')) || []);
const userToEdit = ref(null);

const filterCriteria = ref({});
const sortCriteria = ref(null);

const filteredData = computed(() => {
  const results = data.value
    .filter(user =>
      Object.keys(filterCriteria.value).every(key =>
        String(user[key]).toLowerCase().includes(String(filterCriteria.value[key]).toLowerCase())
      )
    )
    .map(user => ({ ...user }));

  if (sortCriteria.value) {
    const { key, order } = sortCriteria.value;
    results.sort((a, b) => (order === 'asc' ? a[key] - b[key] : b[key] - a[key]));
  }

  return results;
});

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

const applyFilter = (criteria) => {
  filterCriteria.value = Object.fromEntries(
    Object.entries(criteria).filter(([_, value]) => value)
  );
};

const applySort = (criteria) => {
  sortCriteria.value = criteria;
};

const prepareEditUser = (user, index) => {
  userToEdit.value = { ...user, index };
};
</script>
