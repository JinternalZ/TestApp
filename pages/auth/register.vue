<template>
  <div class="min-h-[80vh] flex items-center justify-center">
    <div class="w-full max-w-md">
      <div class="text-center mb-8">
        <h1 class="text-2xl font-bold">Create an Account</h1>
        <p class="text-gray-600 dark:text-gray-400 mt-2">
          Join our community of artists and creators
        </p>
      </div>

      <form @submit.prevent="handleRegister" class="card">
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
            <p class="mt-1 text-xs text-gray-500">
              Must be at least 8 characters
            </p>
          </div>

          <div>
            <label for="confirmPassword" class="label">Confirm Password</label>
            <input
              id="confirmPassword"
              v-model="confirmPassword"
              type="password"
              required
              class="input"
              placeholder="••••••••"
            />
          </div>

          <div class="flex items-start">
            <input
              id="terms"
              v-model="acceptTerms"
              type="checkbox"
              required
              class="mt-1 mr-2"
            />
            <label for="terms" class="text-sm">
              I agree to the
              <NuxtLink to="/terms" class="text-primary-600 hover:text-primary-500">
                Terms of Service
              </NuxtLink>
              and
              <NuxtLink to="/privacy" class="text-primary-600 hover:text-primary-500">
                Privacy Policy
              </NuxtLink>
            </label>
          </div>

          <button type="submit" class="btn-primary w-full" :disabled="loading || !isValid">
            {{ loading ? 'Creating account...' : 'Create account' }}
          </button>
        </div>
      </form>

      <p class="text-center mt-4 text-sm text-gray-600 dark:text-gray-400">
        Already have an account?
        <NuxtLink to="/auth/login" class="text-primary-600 hover:text-primary-500">
          Sign in
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
const confirmPassword = ref('');
const acceptTerms = ref(false);
const loading = ref(false);

const isValid = computed(() => {
  return email.value &&
    password.value.length >= 8 &&
    password.value === confirmPassword.value &&
    acceptTerms.value;
});

const handleRegister = async () => {
  if (!isValid.value) return;

  try {
    loading.value = true;
    const { error } = await client.auth.signUp({
      email: email.value,
      password: password.value
    });

    if (error) throw error;

    // Show success message
    const { useToast } = useNuxtApp().$AppToaster.useToast();
    useToast().success('Account created successfully! You can now log in.');
    
    // Redirect to login
    router.push('/auth/login');
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