<script lang="ts">
// this component will display a small postion of the screen
/*
"
(Rounded Profile Pic) Ronald Smith                               (3pics of rounded profilepics all same) | Mail Button  Call Button More Button
                      Created on Dec 12, 2023

"
*/
</script>

<template>
  <div class="flex items-center justify-between mt-4 mb-4 ml-2 mr-2">
    <div class="flex items-center">
      <NuxtImg
          src="/images/man.jpg"
          width="40"
          height="40"
          class="rounded-full mr-2 ml-2 "
          alt="My avatar"

      />
      <div>
        <div class="text-lg font-semibold">Ronald Smith</div>
        <div class="text-gray-600 text-sm">Created on Dec 12, 2023</div>
      </div>
    </div>
    <div class="flex items-center">
      <div class="flex -space-x-3 mr-4">
        <NuxtImg
            src="/images/man.jpg"
            width="30"
            height="30"
            class="rounded-full "
            alt="My avatar"

        />
        <NuxtImg
            src="/images/man.jpg"
            width="30"
            height="30"
            class="rounded-full "
            alt="My avatar"

        />
        <NuxtImg
            src="/images/man.jpg"
            width="30"
            height="30"
            class="rounded-full"
            alt="My avatar"

        />
      </div>
      <UButton size="md" icon="mdi:email-outline" class="bg-white hover:bg-white focus:bg-white active:bg-white dark:bg-white text-black hover:text-gray-500 dark:hover:text-gray-400 mr-2" />
      <UButton size="md" icon="mdi:phone-outline" class="bg-white hover:bg-white focus:bg-white active:bg-white dark:bg-white text-black hover:text-gray-500 dark:hover:text-gray-400 mr-2" />
      <UButton size="md" icon="mdi:dots-vertical" class="bg-white hover:bg-white focus:bg-white active:bg-white dark:bg-white text-black hover:text-gray-500 dark:hover:text-gray-400" />
    </div>
  </div>
</template>

<style scoped>

</style>