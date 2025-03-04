<script setup lang="ts">
import { romanizedIthkuilToIpa, romanizedIthkuilToSyllables } from 'ithkuil-tools'
import { computed, ref } from 'vue'
import ipaTranslationOptions from './ipa-translation-options.vue'

// Interface

// Local State
const translationOptions = ref({
  brackets: true,
  fullStopsBetweenVowels: true
})

const romanizedIthkuilText = ref('Wezvwaušburdóu yaizxra sai.')
const ipaResult = computed<string | Error>(() => romanizedIthkuilToIpa(romanizedIthkuilText.value, {
  stressMarks: 'line',
  brackets: translationOptions.value.brackets,
  fullStopsBetweenVowels: translationOptions.value.fullStopsBetweenVowels
}))

const ipa = computed<string | undefined>(() => {
  if (typeof ipaResult.value === 'string') {
    return ipaResult.value
  } else {
    return undefined
  }
})

const error = computed<Error | undefined>(() => {
  if (ipaResult.value instanceof Error) {
    return ipaResult.value
  } else {
    return undefined
  }
})

const syllables = computed(() => romanizedIthkuilToSyllables(romanizedIthkuilText.value).map(word => word.join('-')).join(' '))

// Events

// Non-Reactive Properties
</script>

<template>
  <div class="ipa-component">
    <div class="wrapper">
      <h1>Romanized Ithkuil to IPA</h1>

      <input type="text" v-model="romanizedIthkuilText" class="ithkuil" />

      <ipa-translation-options v-model="translationOptions"/>

      <p v-if="ipa">IPA: <span class="ipa">{{ ipa }}</span></p>

      <pre v-if="error" class="ipa error">{{ error }}</pre>

      <p>Syllables: <span class="syllables">{{ syllables }}</span></p>
    </div>
  </div>
</template>

<style scoped>
.error {
  font-size: .8rem;
  color: var(--orange);
}
.ipa {
  font-family: "Source Code Pro", monospace;
  color: var(--magenta);
}
.syllables {
  color: var(--red);
  font-weight: bold;
}
</style>
