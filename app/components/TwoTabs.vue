<script setup lang="ts">
import { ref } from 'vue';

const activeTab = ref('Activity');
</script>

<template>
  <div class="mt-2 ml-3 -mr-2">
    <div class="border-b border-gray-300 w-max">
      <button
          @click="activeTab = 'Deal Info'"
          :class="[
          'pb-2 px-20 font-medium transition-colors',
          activeTab === 'Deal Info'
            ? 'text-gray-900 border-b-2 border-black'
            : 'text-gray-500 border-b-2 border-transparent hover:text-black'
        ]"
      >
        Deal Info
      </button>
      <button
          @click="activeTab = 'Activity'"
          :class="[
          'pb-2 px-20 font-medium transition-colors',
          activeTab === 'Activity'
            ? 'text-gray-900 border-b-2 border-black'
            : 'text-gray-500 border-b-2 border-transparent hover:text-black'
        ]"
      >
        Activity
      </button>
    </div>
  </div>
</template>

<style scoped>
</style>