<template>
  <div class="max-w-2xl mx-auto">
    <div class="text-center mb-12">
      <h1>Join as a Creator</h1>
      <p class="text-lg text-gray-600 dark:text-gray-400 mt-4">
        Find the perfect music for your content
      </p>
    </div>

    <form @submit.prevent="handleSubmit" class="space-y-6">
      <!-- Basic Information -->
      <div class="card">
        <h2 class="text-xl font-semibold mb-4">Basic Information</h2>
        
        <div class="space-y-4">
          <div>
            <label for="creatorName" class="label">Creator Name</label>
            <input
              id="creatorName"
              v-model="form.creatorName"
              type="text"
              required
              class="input"
              placeholder="Your creator name or handle"
            />
          </div>

          <div>
            <label for="contentType" class="label">Primary Content Type</label>
            <select id="contentType" v-model="form.contentType" required class="input">
              <option value="">Select content type</option>
              <option v-for="type in contentTypes" :key="type" :value="type">
                {{ type }}
              </option>
            </select>
          </div>

          <div>
            <label for="bio" class="label">Bio</label>
            <textarea
              id="bio"
              v-model="form.bio"
              rows="4"
              class="input"
              placeholder="Tell us about your content"
            ></textarea>
          </div>
        </div>
      </div>

      <!-- Social Links -->
      <div class="card">
        <h2 class="text-xl font-semibold mb-4">Social Media Links</h2>
        
        <div class="space-y-4">
          <div>
            <label for="tiktok" class="label">TikTok Username</label>
            <input
              id="tiktok"
              v-model="form.tiktok"
              type="text"
              class="input"
              placeholder="@username"
            />
          </div>

          <div>
            <label for="instagram" class="label">Instagram Username</label>
            <input
              id="instagram"
              v-model="form.instagram"
              type="text"
              class="input"
              placeholder="@username"
            />
          </div>

          <div>
            <label for="youtube" class="label">YouTube Channel URL</label>
            <input
              id="youtube"
              v-model="form.youtube"
              type="url"
              class="input"
              placeholder="https://youtube.com/c/..."
            />
          </div>
        </div>
      </div>

      <div class="flex items-start mb-4">
        <input
          id="terms"
          v-model="form.acceptTerms"
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

      <button type="submit" class="btn-primary w-full" :disabled="loading">
        {{ loading ? 'Creating profile...' : 'Create Creator Profile' }}
      </button>
    </form>
  </div>
</template>

<script setup>
const client = useSupabaseClient();
const user = useSupabaseUser();
const router = useRouter();

const contentTypes = [
  'Lifestyle & Vlogs',
  'Dance & Choreography',
  'Comedy & Skits',
  'Gaming',
  'Education & How-to',
  'Fashion & Beauty',
  'Food & Cooking',
  'Travel',
  'Sports & Fitness',
  'Other'
];

const form = reactive({
  creatorName: '',
  contentType: '',
  bio: '',
  tiktok: '',
  instagram: '',
  youtube: '',
  acceptTerms: false
});

const loading = ref(false);

const handleSubmit = async () => {
  if (!user.value) {
    router.push('/auth/register');
    return;
  }

  try {
    loading.value = true;
    
    // Create creator profile in database
    const { error } = await client
      .from('creator_profiles')
      .insert({
        user_id: user.value.id,
        name: form.creatorName,
        content_type: form.contentType,
        bio: form.bio,
        tiktok_handle: form.tiktok,
        instagram_handle: form.instagram,
        youtube_url: form.youtube
      });

    if (error) throw error;

    // Show success message
    const { useToast } = useNuxtApp().$AppToaster.useToast();
    useToast().success('Creator profile created successfully!');
    
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

// Redirect if not logged in
watchEffect(() => {
  if (!user.value) {
    router.push('/auth/register');
  }
});
</script>