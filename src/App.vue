<script setup>
import { RouterView, useRoute } from 'vue-router'
import { ref, watch } from 'vue'

const route = useRoute()
const skipLink = ref()

watch(
  () => route.path,
  () => {
    skipLink.value.focus()
  }
)
</script>

<template>
  <ul class="skip-links">
    <li>
      <a href="#main" ref="skipLink" class="skip-link">Skip to main content</a>
    </li>
  </ul>
  <div class="bg-gradient-to-r dark:from-cadet-gray-950 dark:to-cadet-gray-700 from-cadet-gray-50 to-cadet-gray-200">
    <RouterView />
  </div>
</template>

<style scoped>
.skip-link {
  white-space: nowrap;
  margin: 1em auto;
  top: 0;
  position: fixed;
  left: 50%;
  margin-left: -72px;
  opacity: 0;
}
.skip-link:focus {
  opacity: 1;
  background-color: white;
  padding: 0.5em;
  border: 1px solid black;
}
</style>
