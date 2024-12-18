<template>
  <div id="app">
    <router-view />
    <SpeedInsights />
  </div>
</template>

<script setup>
// No additional setup needed
import { SpeedInsights } from '@vercel/speed-insights/vue';

</script>

<style>
@import "https://cdn.jsdelivr.net/npm/remixicon@3.5.0/fonts/remixicon.css";


#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  display: flex;
  flex-direction: column;
  min-height: 100vh;
}

*{
  margin: 0;
  padding: 0;
}

:root {
  --background: #e5e6e7;
  --text: #333;
  --nav-background: white;
  --card-background: white;
  --card-text: #2c3e50;
  --card-info-background: #f8f9fa;
  --card-info-text: #6c757d;
  --footer-background: #1a202c;
  --footer-text: #a0aec0;
  --footer-border: #2d3748;
  --link-color: #4299e1;
  --link-hover-color: #63b3ed;
}

.dark-mode {
  --background: #0a0a0a;
  --text: #e2e8f0;
  --nav-background: #222;
  --card-background: #222;
  --card-text: #e2e8f0;
  --card-info-background: #222;
  --card-info-text: #cbd5e0;
  --footer-background: #222;
  --footer-text: #cbd5e0;
  --footer-border: #4a5568;
  --link-color: #63b3ed;
  --link-hover-color: #90cdf4;
}

body {
  background: var(--background);
  color: var(--text);
  line-height: 1.6;
  display: flex;
  flex-direction: column;
  min-height: 100vh;
  transition: background-color 0.3s ease, color 0.3s ease;
}

.home {
  flex: 1;
  display: flex;
  flex-direction: column;
}

main {
  flex: 1;
}
</style>

