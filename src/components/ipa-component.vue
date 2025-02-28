<script setup lang="ts">
import { computed, ref } from 'vue'
const { romanizedIthkuilToIpa } = await import('ithkuil-tools')

// Interface

// Local State
const romanizedIthkuilText = ref('Wezvwaušburdóu yaizxra sai.')
const ipaResult = computed<string | Error>(() => romanizedIthkuilToIpa(romanizedIthkuilText.value))

const ipa = computed<string | undefined>(() => {
  if (typeof ipaResult.value === 'string') {
    return ipaResult.value
  } else {
    return undefined
  }
})

const error = computed<string | undefined>(() => {
  if (ipaResult.value instanceof Error) {
    return ipaResult.value
  } else {
    return undefined
  }
})

// Events

// Non-Reactive Properties
</script>

<template>
  <div class="ipa-component">
    <div class="wrapper">
      <h1>Romanized Ithkuil to IPA</h1>
      <input type="text" v-model="romanizedIthkuilText" class="ithkuil" />
      <p v-if="ipa" class="ipa">{{ ipa }}</p>

      <pre v-if="error" class="ipa error" style="text-align: left;">{{ error }}</pre>
    </div>
  </div>
</template>

<style scoped>
.error {
  color: var(--red);
}
</style>
