<template>
  <header class="sticky top-0 z-50 bg-white dark:bg-gray-900 shadow-sm">
    <div class="container mx-auto px-4">
      <div class="flex h-16 items-center justify-between">
        <!-- Logo -->
        <NuxtLink to="/" class="flex items-center space-x-2">
          <span class="text-primary-600 dark:text-primary-400">
            <Icon name="carbon:music" size="32" />
          </span>
          <span class="text-xl font-bold">MusicMatch</span>
        </NuxtLink>

        <!-- Navigation - Desktop -->
        <nav class="hidden md:flex items-center space-x-8">
          <NuxtLink to="/discover" class="text-sm font-medium hover:text-primary-600 transition-colors">
            Discover
          </NuxtLink>
          <NuxtLink to="/how-it-works" class="text-sm font-medium hover:text-primary-600 transition-colors">
            How It Works
          </NuxtLink>
          <NuxtLink to="/pricing" class="text-sm font-medium hover:text-primary-600 transition-colors">
            Pricing
          </NuxtLink>
        </nav>

        <!-- User Actions -->
        <div class="flex items-center space-x-4">
          <ThemeToggle />
          
          <template v-if="user">
            <div class="relative" v-click-outside="closeUserMenu">
              <button @click="toggleUserMenu" class="flex items-center space-x-1 rounded-full">
                <img v-if="user.user_metadata?.avatar_url" :src="user.user_metadata.avatar_url" alt="User avatar"
                  class="h-8 w-8 rounded-full object-cover" />
                <div v-else class="h-8 w-8 rounded-full bg-primary-100 flex items-center justify-center text-primary-700">
                  {{ userInitials }}
                </div>
              </button>

              <div v-if="isUserMenuOpen"
                class="absolute right-0 top-full mt-2 w-48 rounded-md bg-white dark:bg-gray-800 shadow-lg py-1 ring-1 ring-black ring-opacity-5 focus:outline-none">
                <NuxtLink to="/dashboard"
                  class="block px-4 py-2 text-sm hover:bg-gray-100 dark:hover:bg-gray-700">
                  Dashboard
                </NuxtLink>
                <NuxtLink to="/settings"
                  class="block px-4 py-2 text-sm hover:bg-gray-100 dark:hover:bg-gray-700">
                  Settings
                </NuxtLink>
                <button @click="logout"
                  class="block w-full text-left px-4 py-2 text-sm text-error-600 hover:bg-gray-100 dark:hover:bg-gray-700">
                  Sign out
                </button>
              </div>
            </div>
          </template>

          <template v-else>
            <NuxtLink to="/auth/login" class="btn-outline">Log in</NuxtLink>
            <NuxtLink to="/auth/register" class="btn-primary">Sign up</NuxtLink>
          </template>
        </div>
      </div>
    </div>
  </header>
</template>

<script setup>
const user = useSupabaseUser();
const client = useSupabaseClient();
const router = useRouter();

const userInitials = computed(() => {
  if (!user.value) return '';
  const name = user.value.user_metadata?.full_name || user.value.email || '';
  return name
    .split(' ')
    .map(part => part.charAt(0))
    .join('')
    .toUpperCase()
    .substring(0, 2);
});

const isUserMenuOpen = ref(false);

const toggleUserMenu = () => {
  isUserMenuOpen.value = !isUserMenuOpen.value;
};

const closeUserMenu = () => {
  isUserMenuOpen.value = false;
};

const logout = async () => {
  await client.auth.signOut();
  router.push('/');
};

// Directive to detect clicks outside an element
const vClickOutside = {
  mounted(el, binding) {
    el._clickOutside = (event) => {
      if (!(el === event.target || el.contains(event.target))) {
        binding.value(event);
      }
    };
    document.addEventListener('click', el._clickOutside);
  },
  unmounted(el) {
    document.removeEventListener('click', el._clickOutside);
  },
};
</script>