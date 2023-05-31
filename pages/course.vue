<script setup>
import { useCourse } from "../composables/useCourse";

const { chapters } = useCourse();
console.log(useCourse());
const resetError = async (error) => {
  await navigateTo(
    "/course/chapter/1-chapter-1/lesson/1-introduction-to-typescript-with-vue-js-3"
  );
  error.value = null;
};
</script>
<template>
  <div class="prose mb-12">
    <h1>
      <span class="font-medium">
        Course:
        <span class="font-bold">Mastering Nuxt 3</span>
      </span>
    </h1>
  </div>

  <div class="flex flex-row justify-center flex-grow">
    <div
      class="prose mr-4 p-8 bg-white rounded-md min-w-[20ch] max-w-[30ch] flex flex-col"
    >
      <h3>Chapters</h3>
      <!-- All the lessons for the course listed here -->
      <div
        class="space-y-1 mb-4 flex flex-col"
        v-for="chapter in chapters"
        :key="chapter.slug"
      >
        <h4>{{ chapter.title }}</h4>
        <NuxtLink
          v-for="(lesson, index) in chapter.lessons"
          class="flex flex-row space-x-1 no-underline prose-sm font-normal py-1"
          :to="lesson.path"
          :class="{
            'text-blue-500': lesson.path === $route.fullPath,
            'text-gray-600': lesson.path !== $route.fullPath,
          }"
        >
          <span>{{ index + 1 }}.</span>
          <span>{{ lesson.title }}</span>
        </NuxtLink>
      </div>
    </div>

    <div class="prose p-12 bg-white rounded-md w-[65ch]">
      <NuxtErrorBoundary>
        <NuxtPage />
        <template #error="{ error }">
          <p>
            An error occurred while rendering the page. Check developer tools
            for details. <code>{{ error }}</code>
          </p>
          <button
            @click="resetError(error)"
            class="hover:cursor-pointer bg-gray-500 text-white font-bold py-1 px-2 rounded-sm"
          >
            Reset
          </button>
        </template>
      </NuxtErrorBoundary>
    </div>
  </div>
</template>

<style scoped>
.router-link-active {
  @apply text-blue-500;
}
</style>
