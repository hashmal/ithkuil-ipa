<script setup lang="ts">
import IpaComponent from './components/ipa-component.vue'
</script>

<template>
  <Suspense>
    <template #default>
      <IpaComponent />
    </template>
    <template #fallback>
      <div>Loading...</div>
    </template>
  </Suspense>
</template>
