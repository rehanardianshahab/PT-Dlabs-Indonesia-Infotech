<template>
<header class="flex px-8 justify-between items-center w-full bg-gray-800 h-16">
    <div class="text-white font-bold">Landing Page</div>
    <nav class="hidden sm:flex space-x-4">
    <a href="#" class="hover:text-blue-400">Home</a>
    <a href="#" class="hover:text-blue-400">About</a>
    </nav>
    <button class="sm:hidden text-white" @click="toggleMenu">☰</button>
</header>
</template>

<script setup>
const toggleMenu = () => {
const menu = document.querySelector('nav');
menu.classList.toggle('hidden');
};
</script>
  