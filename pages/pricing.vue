<template>
  <div class="max-w-5xl mx-auto">
    <div class="text-center mb-12">
      <h1>Simple, Usage-Based Pricing</h1>
      <p class="text-lg text-gray-600 dark:text-gray-400 mt-4">
        Pay only for what you use. No hidden fees or complicated terms.
      </p>
    </div>

    <div class="grid md:grid-cols-2 gap-8 mb-12">
      <!-- For Creators -->
      <div class="card">
        <div class="text-center mb-8">
          <h2 class="text-2xl font-bold mb-4">For Creators</h2>
          <p class="text-gray-600 dark:text-gray-400">
            Pay per thousand views (CPM)
          </p>
        </div>

        <ul class="space-y-4 mb-8">
          <li class="flex items-start">
            <Icon name="carbon:checkmark" class="w-5 h-5 text-success-500 mr-2 mt-0.5" />
            <span>Pay only for actual video views</span>
          </li>
          <li class="flex items-start">
            <Icon name="carbon:checkmark" class="w-5 h-5 text-success-500 mr-2 mt-0.5" />
            <span>Rates start from $1 per 1000 views</span>
          </li>
          <li class="flex items-start">
            <Icon name="carbon:checkmark" class="w-5 h-5 text-success-500 mr-2 mt-0.5" />
            <span>No upfront costs or subscriptions</span>
          </li>
          <li class="flex items-start">
            <Icon name="carbon:checkmark" class="w-5 h-5 text-success-500 mr-2 mt-0.5" />
            <span>Automatic view tracking across platforms</span>
          </li>
        </ul>

        <NuxtLink to="/creator-signup" class="btn-primary w-full text-center">
          Start Creating
        </NuxtLink>
      </div>

      <!-- For Artists -->
      <div class="card">
        <div class="text-center mb-8">
          <h2 class="text-2xl font-bold mb-4">For Artists</h2>
          <p class="text-gray-600 dark:text-gray-400">
            Earn per thousand views (CPM)
          </p>
        </div>

        <ul class="space-y-4 mb-8">
          <li class="flex items-start">
            <Icon name="carbon:checkmark" class="w-5 h-5 text-success-500 mr-2 mt-0.5" />
            <span>Set your own per-mille view rate</span>
          </li>
          <li class="flex items-start">
            <Icon name="carbon:checkmark" class="w-5 h-5 text-success-500 mr-2 mt-0.5" />
            <span>No listing or hosting fees</span>
          </li>
          <li class="flex items-start">
            <Icon name="carbon:checkmark" class="w-5 h-5 text-success-500 mr-2 mt-0.5" />
            <span>90% revenue share to artists</span>
          </li>
          <li class="flex items-start">
            <Icon name="carbon:checkmark" class="w-5 h-5 text-success-500 mr-2 mt-0.5" />
            <span>Monthly payouts via Stripe</span>
          </li>
        </ul>

        <NuxtLink to="/artist-signup" class="btn-primary w-full text-center">
          Start Earning
        </NuxtLink>
      </div>
    </div>

    <!-- FAQ Section -->
    <section class="mt-16">
      <h2 class="text-2xl font-bold mb-8 text-center">Frequently Asked Questions</h2>
      
      <div class="space-y-4">
        <div class="card">
          <h3 class="text-lg font-semibold mb-2">How are views counted?</h3>
          <p>Views are counted when your video receives a view on TikTok, Instagram, or YouTube, and our system verifies that the licensed song was used at >50% volume for >50% of the video duration.</p>
        </div>
        
        <div class="card">
          <h3 class="text-lg font-semibold mb-2">When do I get charged as a creator?</h3>
          <p>Charges are processed monthly based on the actual views your videos received. You'll only pay for verified views where the song meets our usage criteria.</p>
        </div>
        
        <div class="card">
          <h3 class="text-lg font-semibold mb-2">When do artists get paid?</h3>
          <p>Artists receive monthly payments for all verified views from the previous month. Payments are processed via Stripe on the 1st of each month.</p>
        </div>
        
        <div class="card">
          <h3 class="text-lg font-semibold mb-2">What platforms are supported?</h3>
          <p>We currently support TikTok, Instagram (Reels), and YouTube (Shorts). More platforms will be added in the future.</p>
        </div>
      </div>
    </section>
  </div>
</template>