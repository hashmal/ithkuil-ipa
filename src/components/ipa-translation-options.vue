<script setup lang="ts">

// Interface
const options = defineModel<{
  brackets: boolean,
  fullStopsBetweenVowels: boolean,
}>({required: true})

// Local State

// Events

// Non-Reactive Properties

</script>

<template>
  <div class="ipa-translation-options">
    <label>
      <input type="checkbox" v-model="options.brackets" />
      Brackets
    </label>

    <label>
      <input type="checkbox" v-model="options.fullStopsBetweenVowels" />
      Full stops between syllables
    </label>

  </div>
</template>

<style scoped lang='scss'>
</style>
