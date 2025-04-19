<template>
  <div class="max-w-2xl mx-auto">
    <div class="text-center mb-12">
      <h1>Join as an Artist</h1>
      <p class="text-lg text-gray-600 dark:text-gray-400 mt-4">
        Share your music with creators and earn from every view
      </p>
    </div>

    <form @submit.prevent="handleSubmit" class="space-y-6">
      <!-- Basic Information -->
      <div class="card">
        <h2 class="text-xl font-semibold mb-4">Basic Information</h2>
        
        <div class="space-y-4">
          <div>
            <label for="artistName" class="label">Artist/Band Name</label>
            <input
              id="artistName"
              v-model="form.artistName"
              type="text"
              required
              class="input"
              placeholder="Your artist or band name"
            />
          </div>

          <div>
            <label for="genre" class="label">Primary Genre</label>
            <select id="genre" v-model="form.genre" required class="input">
              <option value="">Select a genre</option>
              <option v-for="genre in genres" :key="genre" :value="genre">
                {{ genre }}
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
              placeholder="Tell us about yourself and your music"
            ></textarea>
          </div>
        </div>
      </div>

      <!-- Social Links -->
      <div class="card">
        <h2 class="text-xl font-semibold mb-4">Social Media Links</h2>
        
        <div class="space-y-4">
          <div>
            <label for="spotify" class="label">Spotify Artist URL</label>
            <input
              id="spotify"
              v-model="form.spotify"
              type="url"
              class="input"
              placeholder="https://open.spotify.com/artist/..."
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
        </div>
      </div>

      <!-- Payment Information -->
      <div class="card">
        <h2 class="text-xl font-semibold mb-4">Payment Information</h2>
        
        <div class="space-y-4">
          <div>
            <label for="defaultRate" class="label">Default Per-Mille View Rate ($)</label>
            <input
              id="defaultRate"
              v-model="form.defaultRate"
              type="number"
              required
              min="0.1"
              step="0.1"
              class="input"
              placeholder="2.50"
            />
            <p class="mt-1 text-sm text-gray-500">
              This is your default rate per 1000 views. You can adjust this per song later.
            </p>
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
        {{ loading ? 'Creating profile...' : 'Create Artist Profile' }}
      </button>
    </form>
  </div>
</template>

<script setup>
const client = useSupabaseClient();
const user = useSupabaseUser();
const router = useRouter();

const genres = [
  'Pop', 'Electronic', 'Hip Hop', 'R&B', 'Rock',
  'Indie', 'Folk', 'Jazz', 'Classical', 'Country'
];

const form = reactive({
  artistName: '',
  genre: '',
  bio: '',
  spotify: '',
  instagram: '',
  defaultRate: 2.50,
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
    
    // Create artist profile in database
    const { error } = await client
      .from('artist_profiles')
      .insert({
        user_id: user.value.id,
        name: form.artistName,
        genre: form.genre,
        bio: form.bio,
        spotify_url: form.spotify,
        instagram_handle: form.instagram,
        default_rate: form.defaultRate
      });

    if (error) throw error;

    // Show success message
    const { useToast } = useNuxtApp().$AppToaster.useToast();
    useToast().success('Artist profile created successfully!');
    
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