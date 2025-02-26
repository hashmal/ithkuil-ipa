<script setup lang="ts">
import { computed, ref } from 'vue'
const { romanizedIthkuilToIpa } = await import('ithkuil-tools')

// Interface

// Local State
const romanizedIthkuilText = ref('Wezvwaušburdóu yaizxra sai.')
const ipa = computed(() => romanizedIthkuilToIpa(romanizedIthkuilText.value))

// Events

// Non-Reactive Properties
</script>

<template>
  <div class="ipa-component">
    <div class="wrapper">
      <h1>Romanized Ithkuil to IPA</h1>
      <input type="text" v-model="romanizedIthkuilText" class="ithkuil" />
      <p class="ipa">{{ ipa }}</p>
    </div>
  </div>
</template>
