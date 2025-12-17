<script setup lang="ts">
// No props needed anymore
</script>

<template>
  <div>
    <div class="flex items-center justify-between mt-2">
      <!-- Search Bar (moved to left) -->
      <div class="flex-1 mx-4">
        <div class="relative w-60">
          <UIcon name="solar:magnifer-broken" class="absolute left-3 top-1/2 transform -translate-y-1/2 text-gray-400" />
          <input type="text" placeholder="Search..." class="w-full pl-10 pr-3 py-2 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-indigo-500" />
        </div>
      </div>

      <!-- Right side buttons -->
      <div class="flex items-center mr-2">
        <UButton size="xl" icon="lets-icons:lightning" class="bg-white hover:bg-white focus:bg-white active:bg-white dark:bg-white text-black hover:text-gray-500 dark:hover:text-gray-400" />
        <UButton size="xl" icon="mdi:account-plus" class="bg-white hover:bg-white focus:bg-white active:bg-white dark:bg-white text-black hover:text-gray-500 dark:hover:text-gray-400" />
        <UButton size="xl" icon="material-symbols:notifications-outline" class="bg-white hover:bg-white focus:bg-white active:bg-white dark:bg-white text-black hover:text-gray-500 dark:hover:text-gray-400" />
      </div>

      <UIcon
          name="fluent:divider-tall-24-filled"
          class="w-8 h-8 rounded-full text-gray-300 mr-2 ml-2"
      />

      <button class="flex items-center focus:outline-none hover:text-gray-500">
        <NuxtImg
            src="/images/trees.jpg"
            width="40"
            height="40"
            class="rounded-full mr-2"
            alt="My avatar"
        />
        <UIcon name="line-md:chevron-down" class="w-5 h-5 rounded-full text-black mr-3 hover:text-gray-500" />
      </button>
    </div>
  </div>
</template>

<style scoped>
</style>