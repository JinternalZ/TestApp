<template>
  <!-- Vue Toastify container -->
</template>

<script setup>
import { toast } from 'vue3-toastify';
import 'vue3-toastify/dist/index.css';

// Make toast available globally through a composable
const useToast = () => {
  const success = (message, options = {}) => {
    return toast.success(message, {
      autoClose: 3000,
      ...options
    });
  };

  const error = (message, options = {}) => {
    return toast.error(message, {
      autoClose: 5000,
      ...options
    });
  };

  const info = (message, options = {}) => {
    return toast.info(message, {
      autoClose: 3000,
      ...options
    });
  };

  const warning = (message, options = {}) => {
    return toast.warning(message, {
      autoClose: 4000,
      ...options
    });
  };

  return {
    success,
    error,
    info,
    warning
  };
};

// Properly expose the composable in script setup
defineExpose({ useToast });
</script>