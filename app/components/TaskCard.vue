<script setup lang="ts">
interface Props {
  title: string
  description?: string
  completed?: boolean
  priority?: 'important' | 'normal'
  creator?: string
}

const props = withDefaults(defineProps<Props>(), {
  description: '',
  completed: false,
  priority: 'normal',
  creator: 'You'
})

const emit = defineEmits(['toggle'])

const handleToggle = () => {
  emit('toggle')
}
</script>

<template>
  <div class="bg-white rounded-lg border border-gray-200 p-5 hover:shadow-sm transition-shadow">
    <!-- Header -->
    <div class="flex items-start justify-between gap-4 mb-3">
      <div class="flex items-start gap-3 flex-1">
        <!-- Checkbox -->
        <button
            @click="handleToggle"
            class="mt-1 w-5 h-5 rounded-full border-2 flex items-center justify-center transition-colors"
            :class="completed ? 'bg-green-500 border-green-500' : 'border-gray-300 hover:border-gray-400'"
        >
          <UIcon
              v-if="completed"
              name="i-heroicons-check"
              class="w-3 h-3 text-white"
          />
        </button>

        <!-- Title & Description -->
        <div class="flex-1">
          <h3 class="text-gray-900 font-medium text-base mb-1">
            {{ title }}
          </h3>
          <p v-if="description" class="text-gray-500 text-sm">
            {{ description }}
          </p>
        </div>
      </div>

      <!-- Due Date -->
      <div class="text-right">
        <p class="text-xs text-gray-500 mb-1">Due Date:</p>
        <p class="text-sm font-medium text-gray-900 whitespace-nowrap">
          Today 12:00 PM
        </p>
      </div>
    </div>

    <!-- Footer -->
    <div class="flex items-center justify-between pt-3 border-t border-gray-100">
      <!-- Creator -->
      <div class="flex items-center gap-2">
        <div class="w-6 h-6 rounded-full bg-gradient-to-br from-blue-400 to-purple-500 flex items-center justify-center">
          <span class="text-white text-xs font-medium">
            {{ creator.charAt(0).toUpperCase() }}
          </span>
        </div>
        <span class="text-sm text-gray-600">
          Created by <span class="text-gray-900">{{ creator }}</span>
        </span>
      </div>

      <!-- Priority & Reminder -->
      <div class="flex items-center gap-2">
        <span
            v-if="priority === 'important'"
            class="px-3 py-1 bg-pink-100 text-pink-700 text-xs font-medium rounded-md flex items-center gap-1"
        >
          <span class="w-1.5 h-1.5 bg-pink-700 rounded-full"></span>
          Important
        </span>
        <UButton
            v-else
            variant="ghost"
            color="gray"
            size="sm"
            class="text-gray-600"
        >
          <UIcon name="i-heroicons-list-bullet" class="w-4 h-4" />
          Priority
        </UButton>

        <UButton
            variant="ghost"
            color="gray"
            size="sm"
            class="text-gray-600"
        >
          <UIcon name="i-heroicons-clock" class="w-4 h-4" />
          Reminder
        </UButton>
      </div>
    </div>
  </div>
</template>

<style scoped>
</style>