<template>
  <div>
    <!-- Header Section -->
    <section class="bg-gradient-to-r from-primary-50 to-secondary-50 dark:from-gray-800 dark:to-gray-900 py-12">
      <div class="container mx-auto px-4">
        <div class="max-w-4xl mx-auto">
          <h1 class="text-3xl md:text-4xl font-bold mb-4">Discover Music</h1>
          <p class="text-lg text-gray-700 dark:text-gray-300 mb-8">
            Find the perfect soundtrack for your short-form videos
          </p>
          
          <!-- Search Bar -->
          <div class="relative mb-8">
            <span class="absolute inset-y-0 left-0 flex items-center pl-3 pointer-events-none">
              <Icon name="carbon:search" class="w-5 h-5 text-gray-500" />
            </span>
            <input 
              type="search" 
              v-model="searchQuery"
              class="w-full p-3 pl-10 rounded-lg border border-gray-300 dark:border-gray-600 dark:bg-gray-800 focus:ring-2 focus:ring-primary-500 focus:border-primary-500" 
              placeholder="Search by song title, artist, or genre..." 
            />
          </div>
          
          <!-- Filters -->
          <div class="flex flex-wrap gap-4 mb-6">
            <div class="w-full md:w-auto">
              <select 
                v-model="filters.genre" 
                class="w-full md:w-48 p-2 rounded-md border border-gray-300 dark:border-gray-600 dark:bg-gray-800"
              >
                <option value="">All Genres</option>
                <option value="Pop">Pop</option>
                <option value="Electronic">Electronic</option>
                <option value="Hip Hop">Hip Hop</option>
                <option value="R&B">R&B</option>
                <option value="Rock">Rock</option>
                <option value="Indie">Indie</option>
                <option value="Folk">Folk</option>
                <option value="Jazz">Jazz</option>
              </select>
            </div>
            
            <div class="w-full md:w-auto">
              <select 
                v-model="filters.mood" 
                class="w-full md:w-48 p-2 rounded-md border border-gray-300 dark:border-gray-600 dark:bg-gray-800"
              >
                <option value="">All Moods</option>
                <option value="Upbeat">Upbeat</option>
                <option value="Chill">Chill</option>
                <option value="Energetic">Energetic</option>
                <option value="Emotional">Emotional</option>
                <option value="Inspirational">Inspirational</option>
                <option value="Dramatic">Dramatic</option>
              </select>
            </div>
            
            <div class="w-full md:w-auto">
              <select 
                v-model="filters.priceRange" 
                class="w-full md:w-48 p-2 rounded-md border border-gray-300 dark:border-gray-600 dark:bg-gray-800"
              >
                <option value="">Any Price</option>
                <option value="0-1">$0 - $1 per 1K views</option>
                <option value="1-3">$1 - $3 per 1K views</option>
                <option value="3-5">$3 - $5 per 1K views</option>
                <option value="5+">$5+ per 1K views</option>
              </select>
            </div>
            
            <div class="w-full md:w-auto">
              <select 
                v-model="sortBy" 
                class="w-full md:w-48 p-2 rounded-md border border-gray-300 dark:border-gray-600 dark:bg-gray-800"
              >
                <option value="popular">Most Popular</option>
                <option value="newest">Newest</option>
                <option value="priceAsc">Price: Low to High</option>
                <option value="priceDesc">Price: High to Low</option>
              </select>
            </div>
          </div>
          
          <!-- Active Filters -->
          <div v-if="hasActiveFilters" class="flex flex-wrap gap-2 mb-6">
            <div 
              v-for="(value, key) in activeFilters" 
              :key="key"
              class="bg-primary-100 dark:bg-primary-900 text-primary-800 dark:text-primary-300 px-3 py-1 rounded-full text-sm flex items-center"
            >
              <span>{{ formatFilterName(key) }}: {{ value }}</span>
              <button @click="removeFilter(key)" class="ml-2">
                <Icon name="carbon:close" class="w-4 h-4" />
              </button>
            </div>
            
            <button 
              @click="clearAllFilters" 
              class="text-sm text-gray-600 dark:text-gray-400 hover:text-primary-600 dark:hover:text-primary-400 underline ml-2"
            >
              Clear all
            </button>
          </div>
        </div>
      </div>
    </section>
    
    <!-- Songs Grid -->
    <section class="py-12">
      <div class="container mx-auto px-4">
        <div v-if="loading" class="flex justify-center items-center py-12">
          <div class="animate-spin rounded-full h-12 w-12 border-t-2 border-b-2 border-primary-600"></div>
        </div>
        
        <div v-else-if="filteredSongs.length === 0" class="text-center py-12">
          <Icon name="carbon:music-note" class="w-16 h-16 mx-auto text-gray-400 mb-4" />
          <h3 class="text-xl font-medium mb-2">No songs found</h3>
          <p class="text-gray-600 dark:text-gray-400 mb-6">Try adjusting your filters or search query</p>
          <button @click="clearAllFilters" class="btn-primary">Clear all filters</button>
        </div>
        
        <div v-else>
          <!-- Results Count -->
          <p class="text-gray-600 dark:text-gray-400 mb-6">
            Showing {{ filteredSongs.length }} songs
          </p>
          
          <!-- Songs Grid -->
          <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 xl:grid-cols-4 gap-6">
            <SongCard v-for="song in filteredSongs" :key="song.id" :song="song" />
          </div>
          
          <!-- Load More -->
          <div v-if="hasMoreSongs" class="text-center mt-12">
            <button @click="loadMore" class="btn-outline">
              Load More
            </button>
          </div>
        </div>
      </div>
    </section>
  </div>
</template>

<script setup>
const searchQuery = ref('');
const filters = reactive({
  genre: '',
  mood: '',
  priceRange: ''
});
const sortBy = ref('popular');
const loading = ref(false);
const page = ref(1);
const limit = 8;

// Mock data for songs
const allSongs = ref([
  {
    id: 1,
    title: 'Summer Breeze',
    artist: 'Coastal Dreams',
    genre: 'Pop',
    mood: 'Upbeat',
    duration: 187,
    pricePerMille: 2.50,
    coverArt: 'https://images.unsplash.com/photo-1470225620780-dba8ba36b745?w=500&h=500&fit=crop',
    createdAt: '2023-10-15',
    popularity: 95
  },
  {
    id: 2,
    title: 'Midnight Drive',
    artist: 'Urban Echo',
    genre: 'Electronic',
    mood: 'Chill',
    duration: 215,
    pricePerMille: 3.00,
    coverArt: 'https://images.unsplash.com/photo-1493225457124-a3eb161ffa5f?w=500&h=500&fit=crop',
    createdAt: '2023-09-22',
    popularity: 87
  },
  {
    id: 3,
    title: 'Golden Hour',
    artist: 'Sunset Collective',
    genre: 'Indie',
    mood: 'Emotional',
    duration: 198,
    pricePerMille: 2.75,
    coverArt: 'https://images.unsplash.com/photo-1525362081669-2b476bb628c3?w=500&h=500&fit=crop',
    createdAt: '2023-11-05',
    popularity: 78
  },
  {
    id: 4,
    title: 'Beat of the City',
    artist: 'Metro Rhythm',
    genre: 'Hip Hop',
    mood: 'Energetic',
    duration: 163,
    pricePerMille: 3.25,
    coverArt: 'https://images.unsplash.com/photo-1459749411175-04bf5292ceea?w=500&h=500&fit=crop',
    createdAt: '2023-12-01',
    popularity: 92
  },
  {
    id: 5,
    title: 'Neon Lights',
    artist: 'Synthwave Collective',
    genre: 'Electronic',
    mood: 'Energetic',
    duration: 210,
    pricePerMille: 4.00,
    coverArt: 'https://images.unsplash.com/photo-1514525253161-7a46d19cd819?w=500&h=500&fit=crop',
    createdAt: '2024-01-10',
    popularity: 85
  },
  {
    id: 6,
    title: 'Whispers',
    artist: 'Echo Chamber',
    genre: 'Folk',
    mood: 'Emotional',
    duration: 195,
    pricePerMille: 2.25,
    coverArt: 'https://images.unsplash.com/photo-1511379938547-c1f69419868d?w=500&h=500&fit=crop',
    createdAt: '2023-08-15',
    popularity: 70
  },
  {
    id: 7,
    title: 'Urban Jungle',
    artist: 'City Soundscapes',
    genre: 'Hip Hop',
    mood: 'Dramatic',
    duration: 178,
    pricePerMille: 3.75,
    coverArt: 'https://images.unsplash.com/photo-1501612780327-45045538702b?w=500&h=500&fit=crop',
    createdAt: '2024-02-05',
    popularity: 88
  },
  {
    id: 8,
    title: 'Daybreak',
    artist: 'Morning Melodies',
    genre: 'Pop',
    mood: 'Inspirational',
    duration: 203,
    pricePerMille: 2.80,
    coverArt: 'https://images.unsplash.com/photo-1508700115892-45ecd05ae2ad?w=500&h=500&fit=crop',
    createdAt: '2023-11-22',
    popularity: 76
  },
  {
    id: 9,
    title: 'Jazz Club',
    artist: 'Blue Note Trio',
    genre: 'Jazz',
    mood: 'Chill',
    duration: 258,
    pricePerMille: 5.50,
    coverArt: 'https://images.unsplash.com/photo-1511192336575-5a79af67a629?w=500&h=500&fit=crop',
    createdAt: '2023-10-05',
    popularity: 65
  },
  {
    id: 10,
    title: 'Electric Dreams',
    artist: 'Neural Network',
    genre: 'Electronic',
    mood: 'Energetic',
    duration: 190,
    pricePerMille: 3.50,
    coverArt: 'https://images.unsplash.com/photo-1496293455970-f8581aae0e3b?w=500&h=500&fit=crop',
    createdAt: '2024-01-25',
    popularity: 81
  },
  {
    id: 11,
    title: 'Memories',
    artist: 'Nostalgia',
    genre: 'R&B',
    mood: 'Emotional',
    duration: 225,
    pricePerMille: 2.90,
    coverArt: 'https://images.unsplash.com/photo-1493225457124-a3eb161ffa5f?w=500&h=500&fit=crop',
    createdAt: '2023-09-12',
    popularity: 79
  },
  {
    id: 12,
    title: 'Indie Vibes',
    artist: 'Acoustic Sessions',
    genre: 'Indie',
    mood: 'Chill',
    duration: 200,
    pricePerMille: 2.25,
    coverArt: 'https://images.unsplash.com/photo-1511671782779-c97d3d27a1d4?w=500&h=500&fit=crop',
    createdAt: '2023-07-30',
    popularity: 72
  }
]);

// Computed property for filtered songs
const filteredSongs = computed(() => {
  let result = [...allSongs.value];
  
  // Apply search query filter
  if (searchQuery.value) {
    const query = searchQuery.value.toLowerCase();
    result = result.filter(song => 
      song.title.toLowerCase().includes(query) || 
      song.artist.toLowerCase().includes(query) ||
      song.genre.toLowerCase().includes(query)
    );
  }
  
  // Apply genre filter
  if (filters.genre) {
    result = result.filter(song => song.genre === filters.genre);
  }
  
  // Apply mood filter
  if (filters.mood) {
    result = result.filter(song => song.mood === filters.mood);
  }
  
  // Apply price range filter
  if (filters.priceRange) {
    const [min, max] = filters.priceRange.split('-');
    if (min && max) {
      result = result.filter(song => song.pricePerMille >= parseFloat(min) && song.pricePerMille <= parseFloat(max));
    } else if (min === '5+') {
      result = result.filter(song => song.pricePerMille >= 5);
    }
  }
  
  // Apply sorting
  switch (sortBy.value) {
    case 'newest':
      result.sort((a, b) => new Date(b.createdAt) - new Date(a.createdAt));
      break;
    case 'priceAsc':
      result.sort((a, b) => a.pricePerMille - b.pricePerMille);
      break;
    case 'priceDesc':
      result.sort((a, b) => b.pricePerMille - a.pricePerMille);
      break;
    case 'popular':
    default:
      result.sort((a, b) => b.popularity - a.popularity);
  }
  
  // Pagination
  return result.slice(0, page.value * limit);
});

// Check if there are more songs to load
const hasMoreSongs = computed(() => {
  return filteredSongs.value.length < allSongs.value.length;
});

// Check if there are active filters
const hasActiveFilters = computed(() => {
  return Object.values(filters).some(value => value !== '') || searchQuery.value !== '';
});

// Get active filters for display
const activeFilters = computed(() => {
  const result = {};
  
  if (searchQuery.value) {
    result.search = searchQuery.value;
  }
  
  Object.entries(filters).forEach(([key, value]) => {
    if (value) {
      result[key] = value;
    }
  });
  
  return result;
});

// Format filter name for display
const formatFilterName = (key) => {
  switch (key) {
    case 'search':
      return 'Search';
    case 'genre':
      return 'Genre';
    case 'mood':
      return 'Mood';
    case 'priceRange':
      return 'Price Range';
    default:
      return key.charAt(0).toUpperCase() + key.slice(1);
  }
};

// Remove a specific filter
const removeFilter = (key) => {
  if (key === 'search') {
    searchQuery.value = '';
  } else {
    filters[key] = '';
  }
};

// Clear all filters
const clearAllFilters = () => {
  searchQuery.value = '';
  Object.keys(filters).forEach(key => {
    filters[key] = '';
  });
  sortBy.value = 'popular';
};

// Load more songs
const loadMore = () => {
  loading.value = true;
  
  // Simulate API call delay
  setTimeout(() => {
    page.value++;
    loading.value = false;
  }, 500);
};

// Simulate initial loading
onMounted(() => {
  loading.value = true;
  
  // Simulate API call delay
  setTimeout(() => {
    loading.value = false;
  }, 800);
});
</script>