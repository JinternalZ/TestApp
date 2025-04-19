<template>
  <div class="min-h-screen flex flex-col">
    <NavBar />
    <div class="flex flex-grow">
      <Sidebar />
      <main class="flex-grow p-6 bg-gray-50 dark:bg-gray-900 overflow-auto">
        <slot />
      </main>
    </div>
  </div>
</template>