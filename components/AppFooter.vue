<template>
  <footer class="bg-gray-100 dark:bg-gray-800 py-12">
    <div class="container mx-auto px-4">
      <div class="grid grid-cols-1 md:grid-cols-4 gap-8">
        <div>
          <div class="flex items-center space-x-2">
            <span class="text-primary-600 dark:text-primary-400">
              <Icon name="carbon:music" size="24" />
            </span>
            <span class="text-lg font-bold">MusicMatch</span>
          </div>
          <p class="mt-4 text-sm text-gray-600 dark:text-gray-400">
            Connecting artists with creators to make great content and fair compensation
          </p>
          <div class="mt-6 flex space-x-4">
            <a href="#" class="text-gray-500 hover:text-primary-600 transition-colors">
              <Icon name="carbon:logo-twitter" size="20" />
            </a>
            <a href="#" class="text-gray-500 hover:text-primary-600 transition-colors">
              <Icon name="carbon:logo-facebook" size="20" />
            </a>
            <a href="#" class="text-gray-500 hover:text-primary-600 transition-colors">
              <Icon name="carbon:logo-instagram" size="20" />
            </a>
            <a href="#" class="text-gray-500 hover:text-primary-600 transition-colors">
              <Icon name="carbon:logo-youtube" size="20" />
            </a>
          </div>
        </div>
        
        <div>
          <h4 class="text-base font-semibold mb-4">For Artists</h4>
          <ul class="space-y-3">
            <li><NuxtLink to="/artist-signup" class="text-sm text-gray-600 dark:text-gray-400 hover:text-primary-600 dark:hover:text-primary-400">Register as Artist</NuxtLink></li>
            <li><NuxtLink to="/upload-music" class="text-sm text-gray-600 dark:text-gray-400 hover:text-primary-600 dark:hover:text-primary-400">Upload Music</NuxtLink></li>
            <li><NuxtLink to="/pricing-guide" class="text-sm text-gray-600 dark:text-gray-400 hover:text-primary-600 dark:hover:text-primary-400">Pricing Guide</NuxtLink></li>
            <li><NuxtLink to="/analytics" class="text-sm text-gray-600 dark:text-gray-400 hover:text-primary-600 dark:hover:text-primary-400">Analytics</NuxtLink></li>
          </ul>
        </div>
        
        <div>
          <h4 class="text-base font-semibold mb-4">For Creators</h4>
          <ul class="space-y-3">
            <li><NuxtLink to="/creator-signup" class="text-sm text-gray-600 dark:text-gray-400 hover:text-primary-600 dark:hover:text-primary-400">Register as Creator</NuxtLink></li>
            <li><NuxtLink to="/discover" class="text-sm text-gray-600 dark:text-gray-400 hover:text-primary-600 dark:hover:text-primary-400">Discover Music</NuxtLink></li>
            <li><NuxtLink to="/license-terms" class="text-sm text-gray-600 dark:text-gray-400 hover:text-primary-600 dark:hover:text-primary-400">License Terms</NuxtLink></li>
            <li><NuxtLink to="/track-videos" class="text-sm text-gray-600 dark:text-gray-400 hover:text-primary-600 dark:hover:text-primary-400">Video Tracking</NuxtLink></li>
          </ul>
        </div>
        
        <div>
          <h4 class="text-base font-semibold mb-4">Resources</h4>
          <ul class="space-y-3">
            <li><NuxtLink to="/help" class="text-sm text-gray-600 dark:text-gray-400 hover:text-primary-600 dark:hover:text-primary-400">Help Center</NuxtLink></li>
            <li><NuxtLink to="/blog" class="text-sm text-gray-600 dark:text-gray-400 hover:text-primary-600 dark:hover:text-primary-400">Blog</NuxtLink></li>
            <li><NuxtLink to="/contact" class="text-sm text-gray-600 dark:text-gray-400 hover:text-primary-600 dark:hover:text-primary-400">Contact Us</NuxtLink></li>
            <li><NuxtLink to="/privacy" class="text-sm text-gray-600 dark:text-gray-400 hover:text-primary-600 dark:hover:text-primary-400">Privacy Policy</NuxtLink></li>
            <li><NuxtLink to="/terms" class="text-sm text-gray-600 dark:text-gray-400 hover:text-primary-600 dark:hover:text-primary-400">Terms of Service</NuxtLink></li>
          </ul>
        </div>
      </div>
      
      <div class="mt-12 border-t border-gray-200 dark:border-gray-700 pt-8 flex flex-col md:flex-row md:justify-between items-center">
        <p class="text-sm text-gray-500 dark:text-gray-400">
          © {{ new Date().getFullYear() }} MusicMatch. All rights reserved.
        </p>
        <div class="mt-4 md:mt-0">
          <p class="text-sm text-gray-500 dark:text-gray-400">
            Crafted with ♥ for creators and artists
          </p>
        </div>
      </div>
    </div>
  </footer>
</template>