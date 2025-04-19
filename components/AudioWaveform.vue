<template>
  <div class="waveform-container">
    <div ref="waveformRef" class="w-full h-full"></div>
    <div class="waveform-progress" :style="{ width: `${progress}%` }"></div>
    
    <div class="absolute bottom-3 left-3 right-3 flex items-center justify-between z-10">
      <button @click="togglePlay" class="bg-white dark:bg-gray-800 rounded-full p-2 shadow-sm">
        <Icon v-if="isPlaying" name="carbon:pause" class="h-5 w-5 text-primary-600" />
        <Icon v-else name="carbon:play" class="h-5 w-5 text-primary-600" />
      </button>
      
      <span class="text-xs font-medium text-white bg-black bg-opacity-50 px-2 py-1 rounded-md">
        {{ currentTime }} / {{ duration }}
      </span>
    </div>
  </div>
</template>

<script setup>
import WaveSurfer from 'wavesurfer.js';

const props = defineProps({
  audioUrl: {
    type: String,
    required: true
  },
  peakData: {
    type: Array,
    default: () => []
  }
});

const waveformRef = ref(null);
const wavesurfer = ref(null);
const isPlaying = ref(false);
const progress = ref(0);
const currentTime = ref('0:00');
const duration = ref('0:00');

onMounted(() => {
  if (process.client && waveformRef.value) {
    wavesurfer.value = WaveSurfer.create({
      container: waveformRef.value,
      waveColor: '#a78bfa',
      progressColor: '#7c3aed',
      cursorColor: 'transparent',
      barWidth: 2,
      barGap: 1,
      barRadius: 2,
      height: 80,
      responsive: true,
      normalize: true,
      partialRender: true
    });
    
    wavesurfer.value.load(props.audioUrl);
    
    if (props.peakData?.length > 0) {
      // Use pre-computed peaks if available
      wavesurfer.value.load(props.audioUrl, props.peakData);
    } else {
      wavesurfer.value.load(props.audioUrl);
    }
    
    // Update time and duration
    wavesurfer.value.on('ready', () => {
      duration.value = formatTime(wavesurfer.value.getDuration());
      currentTime.value = '0:00';
    });
    
    // Update time during playback
    wavesurfer.value.on('audioprocess', () => {
      currentTime.value = formatTime(wavesurfer.value.getCurrentTime());
      progress.value = (wavesurfer.value.getCurrentTime() / wavesurfer.value.getDuration()) * 100;
    });
    
    // Update play state
    wavesurfer.value.on('play', () => {
      isPlaying.value = true;
    });
    
    wavesurfer.value.on('pause', () => {
      isPlaying.value = false;
    });
    
    // Handle finish
    wavesurfer.value.on('finish', () => {
      isPlaying.value = false;
      currentTime.value = duration.value;
      progress.value = 100;
    });
    
    // Handle seeking
    wavesurfer.value.on('seeking', () => {
      currentTime.value = formatTime(wavesurfer.value.getCurrentTime());
      progress.value = (wavesurfer.value.getCurrentTime() / wavesurfer.value.getDuration()) * 100;
    });
  }
});

onBeforeUnmount(() => {
  if (wavesurfer.value) {
    wavesurfer.value.destroy();
  }
});

const togglePlay = () => {
  if (wavesurfer.value) {
    wavesurfer.value.playPause();
  }
};

const formatTime = (timeInSeconds) => {
  const minutes = Math.floor(timeInSeconds / 60);
  const seconds = Math.floor(timeInSeconds % 60);
  return `${minutes}:${seconds.toString().padStart(2, '0')}`;
};
</script>