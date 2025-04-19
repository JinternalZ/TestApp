<template>
  <aside
    :class="[
      'w-64 bg-white dark:bg-gray-800 border-r border-gray-200 dark:border-gray-700',
      isOpen ? 'translate-x-0' : '-translate-x-full md:translate-x-0',
    ]"
    class="fixed md:relative inset-y-0 left-0 z-40 transition-transform duration-200 ease-in-out"
  >
    <div class="h-full flex flex-col overflow-y-auto">
      <div class="p-4 border-b border-gray-200 dark:border-gray-700">
        <div class="text-center">
          <div v-if="userType === 'artist'" class="badge-primary mb-2">Artist Dashboard</div>
          <div v-else class="badge-secondary mb-2">Creator Dashboard</div>
          <h3 class="text-lg font-medium">{{ userName }}</h3>
        </div>
      </div>

      <nav class="flex-1 p-4 space-y-1">
        <!-- Artist Navigation -->
        <template v-if="userType === 'artist'">
          <NuxtLink to="/dashboard"
            class="flex items-center p-2 rounded-md hover:bg-gray-100 dark:hover:bg-gray-700"
            :class="{ 'bg-primary-50 text-primary-700 dark:bg-primary-900 dark:text-primary-300': route.path === '/dashboard' }">
            <Icon name="carbon:dashboard" class="mr-3 h-5 w-5" />
            <span>Dashboard</span>
          </NuxtLink>
          
          <NuxtLink to="/songs"
            class="flex items-center p-2 rounded-md hover:bg-gray-100 dark:hover:bg-gray-700"
            :class="{ 'bg-primary-50 text-primary-700 dark:bg-primary-900 dark:text-primary-300': route.path.startsWith('/songs') }">
            <Icon name="carbon:music-note" class="mr-3 h-5 w-5" />
            <span>My Songs</span>
          </NuxtLink>
          
          <NuxtLink to="/uploads"
            class="flex items-center p-2 rounded-md hover:bg-gray-100 dark:hover:bg-gray-700"
            :class="{ 'bg-primary-50 text-primary-700 dark:bg-primary-900 dark:text-primary-300': route.path === '/uploads' }">
            <Icon name="carbon:upload" class="mr-3 h-5 w-5" />
            <span>Upload</span>
          </NuxtLink>
          
          <NuxtLink to="/artist-analytics"
            class="flex items-center p-2 rounded-md hover:bg-gray-100 dark:hover:bg-gray-700"
            :class="{ 'bg-primary-50 text-primary-700 dark:bg-primary-900 dark:text-primary-300': route.path === '/artist-analytics' }">
            <Icon name="carbon:analytics" class="mr-3 h-5 w-5" />
            <span>Analytics</span>
          </NuxtLink>
          
          <NuxtLink to="/earnings"
            class="flex items-center p-2 rounded-md hover:bg-gray-100 dark:hover:bg-gray-700"
            :class="{ 'bg-primary-50 text-primary-700 dark:bg-primary-900 dark:text-primary-300': route.path === '/earnings' }">
            <Icon name="carbon:money" class="mr-3 h-5 w-5" />
            <span>Earnings</span>
          </NuxtLink>
        </template>

        <!-- Creator Navigation -->
        <template v-else>
          <NuxtLink to="/dashboard"
            class="flex items-center p-2 rounded-md hover:bg-gray-100 dark:hover:bg-gray-700"
            :class="{ 'bg-secondary-50 text-secondary-700 dark:bg-secondary-900 dark:text-secondary-300': route.path === '/dashboard' }">
            <Icon name="carbon:dashboard" class="mr-3 h-5 w-5" />
            <span>Dashboard</span>
          </NuxtLink>
          
          <NuxtLink to="/discover"
            class="flex items-center p-2 rounded-md hover:bg-gray-100 dark:hover:bg-gray-700"
            :class="{ 'bg-secondary-50 text-secondary-700 dark:bg-secondary-900 dark:text-secondary-300': route.path === '/discover' }">
            <Icon name="carbon:search" class="mr-3 h-5 w-5" />
            <span>Discover</span>
          </NuxtLink>
          
          <NuxtLink to="/my-licenses"
            class="flex items-center p-2 rounded-md hover:bg-gray-100 dark:hover:bg-gray-700"
            :class="{ 'bg-secondary-50 text-secondary-700 dark:bg-secondary-900 dark:text-secondary-300': route.path === '/my-licenses' }">
            <Icon name="carbon:document" class="mr-3 h-5 w-5" />
            <span>My Licenses</span>
          </NuxtLink>
          
          <NuxtLink to="/my-videos"
            class="flex items-center p-2 rounded-md hover:bg-gray-100 dark:hover:bg-gray-700"
            :class="{ 'bg-secondary-50 text-secondary-700 dark:bg-secondary-900 dark:text-secondary-300': route.path === '/my-videos' }">
            <Icon name="carbon:video" class="mr-3 h-5 w-5" />
            <span>My Videos</span>
          </NuxtLink>
          
          <NuxtLink to="/creator-analytics"
            class="flex items-center p-2 rounded-md hover:bg-gray-100 dark:hover:bg-gray-700"
            :class="{ 'bg-secondary-50 text-secondary-700 dark:bg-secondary-900 dark:text-secondary-300': route.path === '/creator-analytics' }">
            <Icon name="carbon:analytics" class="mr-3 h-5 w-5" />
            <span>Analytics</span>
          </NuxtLink>
        </template>

        <!-- Common Navigation -->
        <div class="pt-4 mt-4 border-t border-gray-200 dark:border-gray-700">
          <NuxtLink to="/settings"
            class="flex items-center p-2 rounded-md hover:bg-gray-100 dark:hover:bg-gray-700"
            :class="{ 'bg-gray-100 dark:bg-gray-700': route.path === '/settings' }">
            <Icon name="carbon:settings" class="mr-3 h-5 w-5" />
            <span>Settings</span>
          </NuxtLink>
          
          <NuxtLink to="/help"
            class="flex items-center p-2 rounded-md hover:bg-gray-100 dark:hover:bg-gray-700"
            :class="{ 'bg-gray-100 dark:bg-gray-700': route.path === '/help' }">
            <Icon name="carbon:help" class="mr-3 h-5 w-5" />
            <span>Help</span>
          </NuxtLink>
        </div>
      </nav>
    </div>
  </aside>

  <!-- Mobile Toggle -->
  <button @click="toggleSidebar" 
    class="fixed md:hidden bottom-6 right-6 z-50 p-3 rounded-full bg-primary-600 text-white shadow-lg">
    <Icon name="carbon:menu" v-if="!isOpen" class="h-6 w-6" />
    <Icon name="carbon:close" v-else class="h-6 w-6" />
  </button>
</template>

<script setup>
const isOpen = ref(false);
const route = useRoute();
const user = useSupabaseUser();

// In a real application, we'd determine this from the user's profile in the database
const userType = ref('artist'); // or 'creator'

const userName = computed(() => {
  if (!user.value) return 'User';
  return user.value.user_metadata?.full_name || user.value.email || 'User';
});

const toggleSidebar = () => {
  isOpen.value = !isOpen.value;
};

// Close sidebar on route change for mobile
watch(() => route.path, () => {
  isOpen.value = false;
});

// Close sidebar when clicking outside on mobile
onMounted(() => {
  if (process.client) {
    document.addEventListener('click', (e) => {
      const sidebar = document.querySelector('aside');
      const toggleButton = document.querySelector('button[class*="fixed md:hidden"]');
      
      if (isOpen.value && sidebar && !sidebar.contains(e.target) && toggleButton && !toggleButton.contains(e.target)) {
        isOpen.value = false;
      }
    });
  }
});
</script>