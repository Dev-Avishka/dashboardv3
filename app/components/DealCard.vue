<script setup lang="ts">
// This is not a floating card component but will display
/*
|Icon| Category(Grey and Small)
|    | Title ( Emphasized and Black)
 */
// will take in the icon category and title as props


const props = defineProps<{
  icon: string;
  category: string;
  title: string;
}>();
</script>

<template>
  <div class="bg-white dark:bg-white shadow-md rounded-lg p-4 flex items-center space-x-4 mt-4">
    <UIcon
      :name="icon"
    class="w-10 h-10 rounded-full bg-gray-200 dark:bg-gray-200 text-black dark:text-black p-2 fill-current"
    ></UIcon>
    <div class="flex-1">
      <h3 class="text-sm font-medium text-gray-500 dark:text-gray-500">{{ category }}</h3>
      <p class="text-lg font-semibold text-black dark:text-black">{{ title }}</p>
    </div>
  </div>
</template>

<style scoped>

</style>