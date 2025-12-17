<script setup lang="ts">
import { ref } from 'vue';

const isSidebarOpen = ref(true);

const toggleSidebar = () => {
  isSidebarOpen.value = !isSidebarOpen.value;
}

// Sidebar menu items
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
      { label: 'Active Deals', to: '/deals/active' },
      { label: 'Closed Deals', to: '/deals/closed' }
    ]
  },
  { icon: 'i-heroicons-squares-2x2', label: 'Integration', to: '/integration' },
  { icon: 'i-heroicons-queue-list', label: 'Tasks', to: '/tasks' },
];

// User activities data
const userActivities = ref([
  {
    id: 1,
    userName: 'Robert',
    userProfilePic: '/images/man.jpg',
    activity: 'Tagged you in a comment',
    activityTime: 'Today, 2:00 AM'
  },
  {
    id: 2,
    userName: 'Sarah',
    userProfilePic: '/images/man.jpg',
    activity: 'Shared a document with you',
    activityTime: 'Yesterday, 5:30 PM'
  },
  {
    id: 3,
    userName: 'Mike',
    userProfilePic: '/images/man.jpg',
    activity: 'Mentioned you in a task',
    activityTime: 'Yesterday, 3:15 PM'
  }
]);

// Active deals data
const activeDeals = ref([
  {
    id: 1,
    icon: 'material-symbols-light:bar-chart',
    category: 'Sales',
    title: 'Special Deal'
  },
  {
    id: 2,
    icon: 'material-symbols-light:handshake',
    category: 'Partnership',
    title: 'Enterprise Contract'
  },
  {
    id: 3,
    icon: 'material-symbols-light:trending-up',
    category: 'Growth',
    title: 'Market Expansion'
  }
]);

// Tasks data
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
  <div class="flex h-screen">
    <!-- SIDEBAR - Integrated directly here -->
    <aside
        :class="[
        'h-full bg-white border-r border-gray-200 transition-all duration-300 flex flex-col relative',
        isSidebarOpen ? 'w-64' : 'w-0'
      ]"
    >
      <!-- Toggle Button - Positioned on the border -->
      <button
          @click="toggleSidebar"
          class="absolute -right-4 top-1/2 -translate-y-1/2 z-50 w-8 h-8 bg-white border border-gray-300 rounded-full flex items-center justify-center hover:bg-gray-50 shadow-md transition-all"
      >
        <UIcon
            :name="isSidebarOpen ? 'i-heroicons-chevron-left' : 'i-heroicons-chevron-right'"
            class="w-4 h-4 text-gray-600"
        />
      </button>

      <div :class="['overflow-hidden h-full', isSidebarOpen ? 'opacity-100' : 'opacity-0']">
        <!-- Sidebar Header -->
        <div class="p-6 border-b border-gray-200">
          <div class="flex items-center gap-2">
            <div class="w-6 h-6 bg-black rounded-sm flex items-center justify-center">
              <span class="text-white text-xs font-bold">▲</span>
            </div>
            <span class="text-xl font-semibold">PLan</span>
          </div>
        </div>

        <!-- Sidebar Navigation -->
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
      </div>
    </aside>

    <!-- Content area -->
    <div class="flex-1 flex flex-col min-h-0">
      <!-- Navbar -->
      <Navbar />

      <TopBar />
      <Divider />
      <UserBar />
      <Divider />

      <div class="flex flex-1 min-h-0">
        <!-- LEFT: Recent Activity (~40%) -->
        <div class="w-114 flex flex-col border-r border-gray-200 min-h-0">
          <TwoTabs class="shrink-0" />

          <div class="flex-1 flex flex-col overflow-hidden px-5 pt-4">
            <h2 class="text-lg font-medium text-gray-700 mb-3">Recent Activity</h2>

            <div class="flex-1 flex flex-col gap-3 min-h-0">
              <!-- Top scrollable area -->
              <div class="flex-1 overflow-y-auto p-4">
                <UserActivityCard
                    v-for="activity in userActivities"
                    :key="activity.id"
                    :user-name="activity.userName"
                    :user-profile-pic="activity.userProfilePic"
                    :activity="activity.activity"
                    :activity-time="activity.activityTime"
                />
              </div>

              <TableDivider />

              <!-- Bottom scrollable area -->
              <div class="flex-1 overflow-y-auto p-4">
                <h3 class="text-lg font-medium text-gray-700 mb-3">Active Deals</h3>
                <DealCard
                    v-for="deal in activeDeals"
                    :key="deal.id"
                    :icon="deal.icon"
                    :category="deal.category"
                    :title="deal.title"
                />
              </div>
            </div>
          </div>
        </div>

        <!-- RIGHT: Upcoming Tasks (~60%, main area) -->
        <div class="flex-1 flex flex-col min-h-0">
          <NineTabs class="shrink-0 -mt-3" />

          <div class="flex-1 overflow-auto p-6">
            <div class="flex items-center justify-between px-6 py-4">
              <h1 class="text-2xl font-bold text-gray-900">Upcoming Tasks</h1>
              <UButton
                  size="xl"
                  label="Create Task"
                  icon="material-symbols:add"
                  class="h-auto bg-white rounded-none border border-gray-300 hover:bg-gray-300"
              />
            </div>

            <div class="min-h-screen">
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
    </div>
  </div>
</template>

<style scoped>
</style>