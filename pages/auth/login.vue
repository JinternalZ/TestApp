<template>
  <div class="min-h-[80vh] flex items-center justify-center">
    <div class="w-full max-w-md">
      <div class="text-center mb-8">
        <h1 class="text-2xl font-bold">Welcome Back</h1>
        <p class="text-gray-600 dark:text-gray-400 mt-2">
          Sign in to your account
        </p>
      </div>

      <form @submit.prevent="handleLogin" class="card">
        <div class="space-y-4">
          <div>
            <label for="email" class="label">Email</label>
            <input
              id="email"
              v-model="email"
              type="email"
              required
              class="input"
              placeholder="you@example.com"
            />
          </div>

          <div>
            <label for="password" class="label">Password</label>
            <input
              id="password"
              v-model="password"
              type="password"
              required
              class="input"
              placeholder="••••••••"
            />
          </div>

          <div class="flex items-center justify-between">
            <label class="flex items-center">
              <input type="checkbox" v-model="rememberMe" class="mr-2" />
              <span class="text-sm">Remember me</span>
            </label>

            <NuxtLink to="/auth/reset-password" class="text-sm text-primary-600 hover:text-primary-500">
              Forgot password?
            </NuxtLink>
          </div>

          <button type="submit" class="btn-primary w-full" :disabled="loading">
            {{ loading ? 'Signing in...' : 'Sign in' }}
          </button>
        </div>
      </form>

      <p class="text-center mt-4 text-sm text-gray-600 dark:text-gray-400">
        Don't have an account?
        <NuxtLink to="/auth/register" class="text-primary-600 hover:text-primary-500">
          Sign up
        </NuxtLink>
      </p>
    </div>
  </div>
</template>

<script setup>
const client = useSupabaseClient();
const user = useSupabaseUser();
const router = useRouter();

const email = ref('');
const password = ref('');
const rememberMe = ref(false);
const loading = ref(false);

const handleLogin = async () => {
  try {
    loading.value = true;
    const { error } = await client.auth.signInWithPassword({
      email: email.value,
      password: password.value
    });

    if (error) throw error;

    // Redirect to dashboard
    router.push('/dashboard');
  } catch (error) {
    console.error('Error:', error.message);
    // Show error toast
    const { useToast } = useNuxtApp().$AppToaster.useToast();
    useToast().error(error.message);
  } finally {
    loading.value = false;
  }
};

// Redirect if already logged in
watchEffect(() => {
  if (user.value) {
    router.push('/dashboard');
  }
});
</script>