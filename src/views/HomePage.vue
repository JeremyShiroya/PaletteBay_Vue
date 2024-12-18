<template>
  <div class="home">
    <NavComp @search="handleSearch" @themeChanged="handleThemeChange" />
    <MainComp :searchTerm="searchTerm" :isDarkMode="isDarkMode" />
    <FooterComp />
  </div>
</template>

<script setup>
import { ref } from 'vue';
import NavComp from '@/components/NavComp.vue';
import MainComp from "@/components/MainComp.vue";
import FooterComp from '@/components/FooterComp.vue';

const searchTerm = ref('');
const isDarkMode = ref(false);

const handleSearch = (term) => {
  searchTerm.value = term;
};

const handleThemeChange = (darkMode) => {
  isDarkMode.value = darkMode;
};
</script>