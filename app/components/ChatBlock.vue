<script setup lang="ts">
import { computed } from 'vue'

interface Props {
  type?: 'prompt' | 'response'
  label?: string
}

const props = withDefaults(defineProps<Props>(), {
  type: 'prompt',
})

const isPrompt = computed(() => props.type === 'prompt')

const headerLabel = computed(() => {
  if (props.label) return props.label
  return isPrompt.value ? 'PROMPT' : 'AI RESPONSE'
})
</script>

<template>
  <div
    class="my-6 rounded-r-lg p-5 border-l-4 transition-colors rounded-lg"
    :class="[
      isPrompt
        ? 'bg-slate-50/80 dark:bg-slate-900/30 border-slate-400 dark:border-slate-500'
        : 'bg-blue-50/50 dark:bg-blue-950/20 border-blue-600 dark:border-blue-500',
    ]"
  >
    <div
      class="font-bold uppercase mb-2"
      :class="[
        isPrompt ? 'text-slate-600 dark:text-slate-400' : 'text-blue-600 dark:text-blue-400',
      ]"
    >
      {{ headerLabel }}
    </div>
    <div class="prose-chat-content prose dark:prose-invert max-w-none">
      <slot />
    </div>
  </div>
</template>

<style scoped>
.prose-chat-content :deep(p:first-child) {
  margin-top: 0;
}
.prose-chat-content :deep(p:last-child) {
  margin-bottom: 0;
}
</style>
