<template>
  <main class="container">
    <div id="color-grid" class="color-grid">
      <template v-if="filteredColors.length">
        <div
          v-for="(color, index) in filteredColors"
          :key="index"
          class="color-card"
        >
          <h3>{{ color.name }}</h3>
          <div class="color-samples">
            <div class="color-sample" :style="{ background: color.dull }">
              <i :class="color.icon" :style="{ color: color.bright }"></i>
            </div>
            <div
              class="color-sample"
              :style="{ background: color.bright }"
            ></div>
          </div>
          <div class="color-info">
            <span>{{ color.dull }}</span>
            <span>{{ color.bright }}</span>
          </div>
        </div>
      </template>
      <div v-else class="no-results">Color not available</div>
    </div>
  </main>
</template>

<script setup>
import { ref, computed, watch } from 'vue';

const props = defineProps(['searchTerm', 'isDarkMode']);

const colors = ref([
  {
    name: "Red",
    shades: [
      { 
        name: "Red", 
        light: { dull: "#FF000073", bright: "#FF0000" },
        dark: { dull: "#E5393973", bright: "#C85656" },
      },
    ],
    icon: "ri-pinterest-fill",
  },
  {
    name: "Green",
    shades: [
      {
        name: "Green",
        light: { dull: "#23FD7783", bright: "#02A340" },
        dark: { dull: "#1D6A3B", bright: "#04E45A" },
      },
    ],
    icon: "ri-whatsapp-line",
  },
  {
    name: "Blue",
    shades: [
      { 
        name: "Blue", 
        light: { dull: "#2f85E773", bright: "#2563EB" },
        dark: { dull: "#1E3A8A", bright: "#60A5FA" },
      },
    ],
    icon: "ri-twitter-fill",
  },
  {
    name: "Purple",
    shades: [
      {
        name: "Purple",
        light: { dull: "#9370DB73", bright: "#8A2BE2" },
        dark: { dull: "#4B0082", bright: "#B39DDB" },
      },
    ],
    icon: "ri-discord-fill",
  },
  {
    name: "Pink",
    shades: [
      {
        name: "Pink",
        light: { dull: "#FF69B473", bright: "#FF1493" },
        dark: { dull: "#C71585", bright: "#FF69B4" },
      },
    ],
    icon: "ri-dribbble-line",
  },
]);

function hexToRgb(hex) {
  hex = hex.replace(/^#/, "");
  if (hex.length === 3) {
    hex = hex[0] + hex[0] + hex[1] + hex[1] + hex[2] + hex[2];
  }
  const num = parseInt(hex, 16);
  return {
    r: num >> 16,
    g: (num >> 8) & 255,
    b: num & 255,
  };
}

function compareHexColors(hex1, hex2, tolerance = 30) {
  const rgb1 = hexToRgb(hex1);
  const rgb2 = hexToRgb(hex2);
  return (
    Math.abs(rgb1.r - rgb2.r) <= tolerance &&
    Math.abs(rgb1.g - rgb2.g) <= tolerance &&
    Math.abs(rgb1.b - rgb2.b) <= tolerance
  );
}

const filteredColors = computed(() => {
  const term = props.searchTerm.toLowerCase().trim();
  const isHexSearch = term.startsWith("#");
  const hexSearchTerm = isHexSearch ? term : `#${term}`;

  return colors.value.flatMap((colorGroup) =>
    colorGroup.shades
      .filter((shade) => {
        const currentMode = props.isDarkMode ? 'dark' : 'light';
        if (isHexSearch && hexSearchTerm.length >= 4) {
          return (
            compareHexColors(hexSearchTerm, shade[currentMode].bright) ||
            compareHexColors(hexSearchTerm, shade[currentMode].dull.slice(0, -2))
          );
        } else if (!isHexSearch) {
          return (
            shade.name.toLowerCase().includes(term) ||
            colorGroup.name.toLowerCase().includes(term)
          );
        }
        return true; // Show all colors if hex search term is too short
      })
      .map((shade) => {
        const currentMode = props.isDarkMode ? 'dark' : 'light';
        return {
          name: shade.name,
          dull: shade[currentMode].dull,
          bright: shade[currentMode].bright,
          icon: colorGroup.icon,
        };
      })
  );
});

// Watch for changes in isDarkMode and update the colors
watch(() => props.isDarkMode, () => {
  // The computed filteredColors will automatically update when isDarkMode changes
});
</script>

<style scoped>
/* Styles remain unchanged */
.container {
  max-width: 1200px;
  margin: 2rem auto;
  padding: 0 1rem;
  flex-grow: 1;
}

.color-grid {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: 2rem;
}

.color-card {
  background: var(--card-background);
  border-radius: 10px;
  overflow: hidden;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
  transition: all 0.3s ease;
  width: 300px;
}

.color-card:hover {
  transform: translateY(-5px);
  box-shadow: 0 6px 12px rgba(0, 0, 0, 0.15);
}

.color-card h3 {
  text-align: left;
  padding: 1rem;
  font-size: 1.2rem;
  font-weight: 600;
  color: var(--card-text);
}

.color-samples {
  display: flex;
  height: 150px;
}

.color-sample {
  flex: 1;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 2rem;
  color: white;
}

.color-info {
  display: flex;
  justify-content: space-between;
  padding: 1rem;
  background: var(--card-info-background);
  font-size: 0.8rem;
  color: var(--card-info-text);
}

.no-results {
  grid-column: 1 / -1;
  text-align: center;
  padding: 2rem;
  font-size: 1.2rem;
  color: var(--card-info-text);
}

@media (max-width: 1200px) {
  .color-grid {
    grid-template-columns: repeat(3, 1fr);
  }
}

@media (max-width: 900px) {
  .color-grid {
    grid-template-columns: repeat(2, 1fr);
  }
}

@media (max-width: 600px) {
  .color-grid {
    grid-template-columns: 1fr;
  }
}
</style>