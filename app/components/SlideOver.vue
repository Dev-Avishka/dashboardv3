<script setup lang="ts">
import { ref } from 'vue';

defineProps({
  isOpen: Boolean,
});

const dealsOpen = ref(true);
const contactsOpen = ref(false);

const menuItems = [
  { icon: 'i-heroicons-chart-bar', label: 'Overview', to: '/overview' },
  {
    icon: 'i-heroicons-user-group',
    label: 'Contacts',
    expandable: true,
    isOpen: contactsOpen
  },
  {
    icon: 'i-heroicons-hand-raised',
    label: 'Deals',
    expandable: true,
    isOpen: dealsOpen,
    children: [
      { label: 'Active Deals', to: '/deals/active', indent: true },
      { label: 'Closed Deals', to: '/deals/closed', indent: true }
    ]
  },
  { icon: 'i-heroicons-squares-2x2', label: 'Integration', to: '/integration' },
  { icon: 'i-heroicons-queue-list', label: 'Tasks', to: '/tasks' },
];
</script>

<template>
  <aside
      :class="[
      'h-full bg-white border-r border-gray-200 transition-all duration-300 flex flex-col',
      isOpen ? 'w-64' : 'w-0 overflow-hidden'
    ]"
  >
    <div class="p-6 border-b border-gray-200">
      <div class="flex items-center gap-2">
        <div class="w-6 h-6 bg-black rounded-sm flex items-center justify-center">
          <span class="text-white text-xs font-bold">▲</span>
        </div>
        <span class="text-xl font-semibold">PLan</span>
      </div>
    </div>

    <nav class="flex-1 p-4 space-y-1 overflow-y-auto">
      <template v-for="item in menuItems" :key="item.label">
        <div v-if="item.expandable">
          <button
              @click="item.isOpen.value = !item.isOpen.value"
              class="w-full flex items-center justify-between px-3 py-2.5 text-gray-600 hover:bg-gray-100 rounded-lg transition-colors"
          >
            <div class="flex items-center gap-3">
              <UIcon :name="item.icon" class="w-5 h-5" />
              <span class="text-sm font-medium">{{ item.label }}</span>
            </div>
            <UIcon
                :name="item.isOpen.value ? 'i-heroicons-chevron-up' : 'i-heroicons-chevron-down'"
                class="w-4 h-4"
            />
          </button>

          <div v-if="item.children && item.isOpen.value" class="mt-1 space-y-1">
            <NuxtLink
                v-for="child in item.children"
                :key="child.label"
                :to="child.to"
                class="flex items-center gap-3 px-3 py-2.5 pl-12 text-gray-600 hover:bg-gray-100 rounded-lg transition-colors text-sm"
            >
              {{ child.label }}
            </NuxtLink>
          </div>
        </div>

        <NuxtLink
            v-else
            :to="item.to"
            class="flex items-center gap-3 px-3 py-2.5 text-gray-600 hover:bg-gray-100 rounded-lg transition-colors"
        >
          <UIcon :name="item.icon" class="w-5 h-5" />
          <span class="text-sm font-medium">{{ item.label }}</span>
        </NuxtLink>
      </template>
    </nav>
  </aside>
</template>

<style scoped>
</style>