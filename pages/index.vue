<template>
  <div>
    <!-- Hero Section -->
    <section class="relative py-20 lg:py-32 overflow-hidden">
      <!-- Background gradient -->
      <div class="absolute inset-0 bg-gradient-to-br from-primary-50 to-secondary-50 dark:from-primary-950 dark:to-secondary-950"></div>
      
      <!-- Abstract shapes -->
      <div class="absolute inset-0 overflow-hidden">
        <div class="absolute -top-32 -right-32 w-96 h-96 rounded-full bg-primary-200 mix-blend-multiply dark:bg-primary-800 dark:mix-blend-overlay opacity-70 blur-3xl"></div>
        <div class="absolute -bottom-32 -left-32 w-96 h-96 rounded-full bg-secondary-200 mix-blend-multiply dark:bg-secondary-800 dark:mix-blend-overlay opacity-70 blur-3xl"></div>
      </div>
      
      <!-- Content -->
      <div class="relative container mx-auto px-4">
        <div class="max-w-3xl mx-auto text-center">
          <h1 class="text-4xl md:text-5xl lg:text-6xl font-bold mb-6 bg-clip-text text-transparent bg-gradient-to-r from-primary-700 to-secondary-700 dark:from-primary-400 dark:to-secondary-400 animate-fade-in">
            Music Licensing Made Simple
          </h1>
          
          <p class="text-lg md:text-xl mb-8 text-gray-700 dark:text-gray-300 animate-slide-up">
            Connect artists with video creators, track usage, and automate payments. 
            The fair and transparent way to license music for short-form videos.
          </p>
          
          <div class="flex flex-col sm:flex-row gap-4 justify-center mb-12">
            <NuxtLink to="/artist-signup" class="btn-primary text-base py-3 px-8">
              Join as Artist
            </NuxtLink>
            <NuxtLink to="/creator-signup" class="btn-secondary text-base py-3 px-8">
              Join as Creator
            </NuxtLink>
          </div>
          
          <!-- Stats -->
          <div class="grid grid-cols-2 md:grid-cols-4 gap-6 text-center mt-12">
            <div class="p-4">
              <p class="text-3xl font-bold text-primary-700 dark:text-primary-400">10K+</p>
              <p class="text-sm text-gray-600 dark:text-gray-400">Songs Available</p>
            </div>
            <div class="p-4">
              <p class="text-3xl font-bold text-primary-700 dark:text-primary-400">2.5K+</p>
              <p class="text-sm text-gray-600 dark:text-gray-400">Artists</p>
            </div>
            <div class="p-4">
              <p class="text-3xl font-bold text-primary-700 dark:text-primary-400">25K+</p>
              <p class="text-sm text-gray-600 dark:text-gray-400">Video Creators</p>
            </div>
            <div class="p-4">
              <p class="text-3xl font-bold text-primary-700 dark:text-primary-400">5M+</p>
              <p class="text-sm text-gray-600 dark:text-gray-400">Views Tracked</p>
            </div>
          </div>
        </div>
      </div>
    </section>
    
    <!-- How It Works Section -->
    <section class="py-20">
      <div class="container mx-auto px-4">
        <div class="text-center mb-12">
          <h2 class="text-3xl md:text-4xl font-bold mb-4">How It Works</h2>
          <p class="text-lg text-gray-600 dark:text-gray-400 max-w-2xl mx-auto">
            Our platform connects artists with video creators, making music licensing transparent, fair, and simple.
          </p>
        </div>
        
        <div class="grid md:grid-cols-3 gap-8 max-w-5xl mx-auto">
          <!-- For Artists -->
          <div class="card text-center flex flex-col items-center">
            <div class="w-16 h-16 rounded-full bg-primary-100 flex items-center justify-center mb-4">
              <Icon name="carbon:music" class="w-8 h-8 text-primary-600" />
            </div>
            <h3 class="text-xl font-bold mb-2">For Artists</h3>
            <p class="text-gray-600 dark:text-gray-400">
              Upload your music, set per-mille view rates, and get paid when creators use your songs.
            </p>
            <ul class="mt-4 text-left space-y-2">
              <li class="flex items-start">
                <Icon name="carbon:checkmark" class="w-5 h-5 text-success-500 mr-2 mt-0.5" />
                <span>Easy uploads & metadata</span>
              </li>
              <li class="flex items-start">
                <Icon name="carbon:checkmark" class="w-5 h-5 text-success-500 mr-2 mt-0.5" />
                <span>Set your own rates</span>
              </li>
              <li class="flex items-start">
                <Icon name="carbon:checkmark" class="w-5 h-5 text-success-500 mr-2 mt-0.5" />
                <span>Track usage & views</span>
              </li>
              <li class="flex items-start">
                <Icon name="carbon:checkmark" class="w-5 h-5 text-success-500 mr-2 mt-0.5" />
                <span>Automated payments</span>
              </li>
            </ul>
          </div>
          
          <!-- For Creators -->
          <div class="card text-center flex flex-col items-center">
            <div class="w-16 h-16 rounded-full bg-secondary-100 flex items-center justify-center mb-4">
              <Icon name="carbon:video" class="w-8 h-8 text-secondary-600" />
            </div>
            <h3 class="text-xl font-bold mb-2">For Creators</h3>
            <p class="text-gray-600 dark:text-gray-400">
              Find the perfect track, license with a click, and earn from your content.
            </p>
            <ul class="mt-4 text-left space-y-2">
              <li class="flex items-start">
                <Icon name="carbon:checkmark" class="w-5 h-5 text-success-500 mr-2 mt-0.5" />
                <span>Browse by genre, mood, BPM</span>
              </li>
              <li class="flex items-start">
                <Icon name="carbon:checkmark" class="w-5 h-5 text-success-500 mr-2 mt-0.5" />
                <span>Preview before licensing</span>
              </li>
              <li class="flex items-start">
                <Icon name="carbon:checkmark" class="w-5 h-5 text-success-500 mr-2 mt-0.5" />
                <span>Simple licensing terms</span>
              </li>
              <li class="flex items-start">
                <Icon name="carbon:checkmark" class="w-5 h-5 text-success-500 mr-2 mt-0.5" />
                <span>Link once, track forever</span>
              </li>
            </ul>
          </div>
          
          <!-- How We Track -->
          <div class="card text-center flex flex-col items-center">
            <div class="w-16 h-16 rounded-full bg-accent-100 flex items-center justify-center mb-4">
              <Icon name="carbon:chart-line" class="w-8 h-8 text-accent-600" />
            </div>
            <h3 class="text-xl font-bold mb-2">Smart Tracking</h3>
            <p class="text-gray-600 dark:text-gray-400">
              Our technology verifies song usage to ensure fair compensation.
            </p>
            <ul class="mt-4 text-left space-y-2">
              <li class="flex items-start">
                <Icon name="carbon:checkmark" class="w-5 h-5 text-success-500 mr-2 mt-0.5" />
                <span>Verifies 50%+ song volume</span>
              </li>
              <li class="flex items-start">
                <Icon name="carbon:checkmark" class="w-5 h-5 text-success-500 mr-2 mt-0.5" />
                <span>Confirms 50%+ video duration</span>
              </li>
              <li class="flex items-start">
                <Icon name="carbon:checkmark" class="w-5 h-5 text-success-500 mr-2 mt-0.5" />
                <span>Tracks across TikTok, IG, YouTube</span>
              </li>
              <li class="flex items-start">
                <Icon name="carbon:checkmark" class="w-5 h-5 text-success-500 mr-2 mt-0.5" />
                <span>Real-time view counting</span>
              </li>
            </ul>
          </div>
        </div>
      </div>
    </section>
    
    <!-- Featured Songs -->
    <section class="py-20 bg-gray-50 dark:bg-gray-900">
      <div class="container mx-auto px-4">
        <div class="flex flex-col md:flex-row md:items-center md:justify-between mb-10">
          <div>
            <h2 class="text-3xl md:text-4xl font-bold">Featured Songs</h2>
            <p class="text-lg text-gray-600 dark:text-gray-400 mt-2">
              Discover trending music that creators love
            </p>
          </div>
          
          <NuxtLink to="/discover" class="btn-primary mt-4 md:mt-0">
            Explore All Music
          </NuxtLink>
        </div>
        
        <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-4 gap-6">
          <SongCard v-for="song in featuredSongs" :key="song.id" :song="song" />
        </div>
      </div>
    </section>
    
    <!-- Testimonials -->
    <section class="py-20">
      <div class="container mx-auto px-4">
        <div class="text-center mb-12">
          <h2 class="text-3xl md:text-4xl font-bold mb-4">Success Stories</h2>
          <p class="text-lg text-gray-600 dark:text-gray-400 max-w-2xl mx-auto">
            Hear from artists and creators who've found success on our platform
          </p>
        </div>
        
        <div class="grid md:grid-cols-2 gap-8 max-w-4xl mx-auto">
          <!-- Artist Testimonial -->
          <div class="card">
            <div class="flex items-start mb-6">
              <div class="flex-shrink-0 mr-4">
                <div class="w-12 h-12 rounded-full bg-primary-100 flex items-center justify-center">
                  <span class="text-xl font-bold text-primary-600">A</span>
                </div>
              </div>
              <div>
                <p class="font-bold">Alex Thompson</p>
                <p class="text-sm text-gray-600 dark:text-gray-400">Independent Artist</p>
              </div>
            </div>
            <blockquote class="text-gray-700 dark:text-gray-300 italic">
              "My music was discovered by a creator with 2M followers who licensed three of my tracks. The exposure led to a 400% increase in my streaming numbers, and I earned over $6,000 in just three months from video views."
            </blockquote>
          </div>
          
          <!-- Creator Testimonial -->
          <div class="card">
            <div class="flex items-start mb-6">
              <div class="flex-shrink-0 mr-4">
                <div class="w-12 h-12 rounded-full bg-secondary-100 flex items-center justify-center">
                  <span class="text-xl font-bold text-secondary-600">J</span>
                </div>
              </div>
              <div>
                <p class="font-bold">Jamie Wilson</p>
                <p class="text-sm text-gray-600 dark:text-gray-400">TikTok Creator</p>
              </div>
            </div>
            <blockquote class="text-gray-700 dark:text-gray-300 italic">
              "Finding music for my content used to be a headache. Now I can discover unique tracks that match my brand perfectly, and I love supporting artists directly. The song I licensed went viral and helped me grow my following by 30% in a month!"
            </blockquote>
          </div>
        </div>
      </div>
    </section>
    
    <!-- CTA Section -->
    <section class="py-20 relative overflow-hidden">
      <div class="absolute inset-0 bg-gradient-to-r from-primary-600 to-secondary-600 dark:from-primary-800 dark:to-secondary-800"></div>
      
      <div class="relative container mx-auto px-4 text-center">
        <h2 class="text-3xl md:text-4xl font-bold mb-4 text-white">Ready to transform your music career?</h2>
        <p class="text-lg text-white text-opacity-90 max-w-2xl mx-auto mb-8">
          Join thousands of artists and creators who are changing the way music licensing works.
        </p>
        
        <div class="flex flex-col sm:flex-row gap-4 justify-center">
          <NuxtLink to="/artist-signup" class="btn bg-white text-primary-700 hover:bg-gray-100 text-base py-3 px-8">
            Sign Up as Artist
          </NuxtLink>
          <NuxtLink to="/creator-signup" class="btn bg-white text-secondary-700 hover:bg-gray-100 text-base py-3 px-8">
            Sign Up as Creator
          </NuxtLink>
        </div>
      </div>
    </section>
  </div>
</template>

<script setup>
// Mock data for featured songs
const featuredSongs = ref([
  {
    id: 1,
    title: 'Summer Breeze',
    artist: 'Coastal Dreams',
    genre: 'Pop',
    duration: 187,
    pricePerMille: 2.50,
    coverArt: 'https://images.unsplash.com/photo-1470225620780-dba8ba36b745?w=500&h=500&fit=crop'
  },
  {
    id: 2,
    title: 'Midnight Drive',
    artist: 'Urban Echo',
    genre: 'Electronic',
    duration: 215,
    pricePerMille: 3.00,
    coverArt: 'https://images.unsplash.com/photo-1493225457124-a3eb161ffa5f?w=500&h=500&fit=crop'
  },
  {
    id: 3,
    title: 'Golden Hour',
    artist: 'Sunset Collective',
    genre: 'Indie',
    duration: 198,
    pricePerMille: 2.75,
    coverArt: 'https://images.unsplash.com/photo-1525362081669-2b476bb628c3?w=500&h=500&fit=crop'
  },
  {
    id: 4,
    title: 'Beat of the City',
    artist: 'Metro Rhythm',
    genre: 'Hip Hop',
    duration: 163,
    pricePerMille: 3.25,
    coverArt: 'https://images.unsplash.com/photo-1459749411175-04bf5292ceea?w=500&h=500&fit=crop'
  }
]);
</script>