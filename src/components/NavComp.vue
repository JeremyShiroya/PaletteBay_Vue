<template>
  <nav>
    <div class="nav-container">
      <div class="nav-left">
        <img src="/Logo.png" alt="Palette Bay Logo" />
        <h1><span class="highlight">Palette</span>Bay</h1>
      </div>
      <div class="nav-center">
        <input
          type="search"
          placeholder="Search Color..."
          v-model="searchTerm"
          @input="$emit('search', searchTerm)"
        />
      </div>
      <div class="nav-right">
        <button
          id="theme-toggle"
          aria-label="Toggle dark mode"
          @click="toggleTheme"
        >
          <i :class="['uil', isDarkMode ? 'uil-sun' : 'uil-moon']"></i>
        </button>
      </div>
    </div>
  </nav>
</template>

<script setup>
import { ref, onMounted } from "vue";

const searchTerm = ref("");
const isDarkMode = ref(false);
const emit = defineEmits(["search", "themeChanged"]);

const toggleTheme = () => {
  isDarkMode.value = !isDarkMode.value;
  emit("themeChanged", isDarkMode.value);
};

onMounted(() => {
  const savedTheme = localStorage.getItem("theme");
  isDarkMode.value = savedTheme === "dark";
  emit("themeChanged", isDarkMode.value);
});
</script>

<style scoped>
/* Add the nav-related styles here */
nav {
  background: var(--nav-background);
  box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
  position: sticky;
  top: 0;
  z-index: 1000;
  transition: background-color 0.3s ease;
}

.nav-container {
  max-width: 1200px;
  margin: 0 auto;
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 0.5rem;
  height: 70px;
}

.nav-left {
  display: none;
  align-items: center;
}

img {
  height: 130px;
  width: auto;
  object-fit: contain;
}

.nav-left h1 {
  font-size: 24px;
  font-weight: 700;
  color: var(--text);
}

.highlight {
  color: #2563eb;
}

.nav-center input {
  padding: 0.5rem 1rem;
  border: 1px solid #e0e0e0;
  border-radius: 20px;
  font-size: 0.9rem;
  width: 250px;
  transition: all 0.3s ease;
  background-color: var(--card-background);
  color: var(--text);
}

.nav-center input:focus {
  outline: none;
  box-shadow: 0 0 0 2px rgba(37, 99, 235, 0.2);
}

.nav-right {
  display: flex;
  align-items: center;
}

#theme-toggle {
  background: none;
  border: none;
  cursor: pointer;
  font-size: 1.5rem;
  color: var(--text);
  transition: color 0.3s ease;
}

#theme-toggle:hover {
  color: #2563eb;
}

/* Add responsive styles here */
@media (max-width: 600px) {
  .nav-container {
    gap: 0.5rem;
  }

  .nav-left {
    display: none;
    width: 70px;
  }

  .nav-left h1 {
    font-size: 17px;
    display: none;
  }

  img {
    margin-left: -15px;
    width: 100px;
  }

  .nav-center input {
    width: 100%;
  }
}
</style>
