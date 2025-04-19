<template>
  <button 
    @click="toggleTheme" 
    class="p-2 rounded-md hover:bg-gray-100 dark:hover:bg-gray-800 focus:outline-none"
    aria-label="Toggle theme"
  >
    <Icon v-if="isDark" name="carbon:moon" class="h-5 w-5" />
    <Icon v-else name="carbon:sun" class="h-5 w-5" />
  </button>
</template>

<script setup>
const colorMode = useColorMode();
const isDark = computed(() => colorMode.value === 'dark');

const toggleTheme = () => {
  colorMode.preference = colorMode.value === 'dark' ? 'light' : 'dark';
};
</script>