<script setup lang="ts">
import { ref } from 'vue';
const isOpen = ref(false);
const Open = () => {
  isOpen.value = true;
}

const tasks = ref([
  {
    id: 1,
    title: 'Share Current letter of employment',
    description: 'There should be three safety seals around the edges of the filter.',
    completed: true,
    priority: 'normal' as const,
    creator: 'You'
  },
  {
    id: 2,
    title: 'Confirmation of income tax payment',
    description: 'Confirmation of property tax payment made up to date',
    completed: false,
    priority: 'important' as const,
    creator: 'Wade Warren'
  },
  {
    id: 3,
    title: 'Confirmation of income tax payment',
    description: 'Confirmation of property tax payment made up to date',
    completed: false,
    priority: 'normal' as const,
    creator: 'Wade Warren'
  }
])

const handleToggle = (id: number) => {
  const task = tasks.value.find(t => t.id === id)
  if (task) {
    task.completed = !task.completed
  }
}
</script>

<template>
  <Navbar :onMenuClick="Open" />
  <SlideOver v-model:isOpen="isOpen" />
  <TopBar />
  <Divider />
  <UserBar />
  <Divider />

  <div class="flex h-[calc(100vh-theme(spacing.32))] min-h-0">
    <!-- LEFT: Recent Activity (~40%) -->
    <div class="w-114 flex flex-col border-r border-gray-200 min-h-0">
      <TwoTabs class="shrink-0" />

      <div class="flex-1 flex flex-col overflow-hidden px-5 pt-4">
        <h2 class="text-lg font-medium text-gray-700 mb-3">Recent Activity</h2>

        <div class="flex-1 flex flex-col gap-3 min-h-0">
          <!-- Top scrollable area -->
          <div class="flex-1 overflow-y-auto p-4">
            <UserActivityCard user-name="Robert" user-profile-pic="/images/man.jpg"
                              activity="Tagged you in a comment" activity-time="Today, 2:00 AM" />
            <UserActivityCard user-name="Robert" user-profile-pic="/images/man.jpg"
                              activity="Tagged you in a comment" activity-time="Today, 2:00 AM" />
            <!-- repeat as needed -->
          </div>

          <TableDivider />

          <!-- Bottom scrollable area -->
          <div class="flex-1 overflow-y-auto p-4">
            <h3 class="text-lg font-medium text-gray-700 mb-3">Active Deals</h3>
            <DealCard icon="material-symbols-light:bar-chart" category="Sales" title="Special Deal" />
            <!-- more deals -->
          </div>
        </div>
      </div>
    </div>

    <!-- RIGHT: Upcoming Tasks (~60%, main area) -->
    <div class="flex-1 flex flex-col min-h-0">
      <NineTabs class="shrink-0 -mt-3" />


      <div class="flex-1 overflow-auto p-6">
        <div class="flex items-center justify-between px-6 py-4 ">
          <h1 class="text-2xl font-bold text-gray-900">Upcoming Tasks</h1>
          <UButton
              size="xl"
              label="Create Task"
              icon="material-symbols:add"
              class="h-auto bg-white rounded-none border border-gray-300 hover:bg-gray-300"
          />
        </div>

        <div class="min-h-screen ">
          <div class="max-w-4xl mx-auto px-4">


            <div class="space-y-4">
              <TaskCard
                  v-for="task in tasks"
                  :key="task.id"
                  :title="task.title"
                  :description="task.description"
                  :completed="task.completed"
                  :priority="task.priority"
                  :creator="task.creator"
                  @toggle="handleToggle(task.id)"
              />
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
</style>