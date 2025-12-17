<script setup lang="ts">

const props = defineProps<{
  userName: string;
  userProfilePic: string;
  activityTime: string;
  activity: string;
}>();
</script>
<template>
  <div class="bg-white dark:bg-white shadow-md rounded-lg p-4 flex items-center space-x-4 mt-4">
<!--    <img :src="userProfilePic" alt="Profile Picture" class="w-16 h-16 rounded-full object-cover" />-->
    <NuxtImg
        v-bind:src="userProfilePic"
        width="30"
        height="30"
        class="rounded-full"
        alt="My avatar"

    />
    <div class="flex-1">
      <h3 class="text-lg font-semibold text-black dark:text-black">{{ userName }}</h3>
      <p class="text-gray-600 dark:text-gray-600">{{ activityTime }}</p>
    </div>
    <div class="text-right">
      <p class="text-black dark:text-black">{{ activity }}</p>
    </div>
  </div>
</template>

<style scoped>

</style>