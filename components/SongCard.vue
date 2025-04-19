<template>
  <div class="card group overflow-hidden">
    <div class="aspect-square relative overflow-hidden rounded-md mb-4 bg-gray-200 dark:bg-gray-700">
      <img :src="song.coverArt" alt="Song artwork" class="w-full h-full object-cover transition-transform duration-300 group-hover:scale-105" />
      
      <button 
        @click="togglePlay"
        class="absolute inset-0 flex items-center justify-center bg-black bg-opacity-20 opacity-0 group-hover:opacity-100 transition-opacity duration-300"
      >
        <span class="bg-white dark:bg-gray-800 rounded-full p-3 shadow-lg">
          <Icon v-if="isPlaying" name="carbon:pause-filled" class="h-8 w-8 text-primary-600" />
          <Icon v-else name="carbon:play-filled" class="h-8 w-8 text-primary-600" />
        </span>
      </button>
    </div>
    
    <div>
      <h3 class="font-bold text-lg">{{ song.title }}</h3>
      <p class="text-sm text-gray-600 dark:text-gray-400">{{ song.artist }}</p>
      
      <div class="mt-3 flex items-center text-sm text-gray-700 dark:text-gray-300">
        <Icon name="carbon:music" class="h-4 w-4 mr-1" />
        <span>{{ song.genre }}</span>
        
        <span class="mx-2">•</span>
        
        <Icon name="carbon:time" class="h-4 w-4 mr-1" />
        <span>{{ formatDuration(song.duration) }}</span>
      </div>
      
      <div class="mt-4 flex items-center justify-between">
        <span class="font-medium text-primary-600 dark:text-primary-400">${{ song.pricePerMille }} per 1K views</span>
        
        <button class="btn-primary">
          License
        </button>
      </div>
    </div>
  </div>
</template>

<script setup>
defineProps({
  song: {
    type: Object,
    required: true
  }
});

const isPlaying = ref(false);

const togglePlay = () => {
  isPlaying.value = !isPlaying.value;
  // Actual audio playback would happen here
};

const formatDuration = (seconds) => {
  const minutes = Math.floor(seconds / 60);
  const remainingSeconds = Math.floor(seconds % 60);
  return `${minutes}:${remainingSeconds.toString().padStart(2, '0')}`;
};
</script>