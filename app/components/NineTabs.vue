<script setup lang="ts">
//nine tabs
import { ref } from 'vue';

const tabs = [
  'Details',
  'Position',
  'Documents',
  'Assessment',
  'Notes',
  'Tasks',
  'Emails',
  'Calls',
  'SMS'
];

const activeTab = ref('Documents');
</script>

<template>
  <div class="border-b border-gray-200 dark:border-gray-200">
    <nav class="-mb-px flex space-x-8 px-6" aria-label="Tabs">
      <button
          v-for="tab in tabs"
          :key="tab"
          @click="activeTab = tab"
          :class="[
          'whitespace-nowrap py-4 px-1 border-b-2 font-medium text-sm transition-colors',
          activeTab === tab
            ? 'border-indigo-500 text-indigo-600'
            : 'border-transparent text-gray-500 hover:text-gray-700 hover:border-gray-300'
        ]"
          :aria-current="activeTab === tab ? 'page' : undefined"
      >
        {{ tab }}
      </button>
    </nav>
  </div>
</template>

<style scoped>
</style>