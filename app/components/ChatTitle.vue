<script setup lang="ts">
interface Props {
  num: number
  img?: string
  icon?: string
  aiName: string
  label: string
  platform?: string
}

defineProps<Props>()

const labelToId = (label: string) => label.toLowerCase().replace(/\s+/g, '-')
</script>

<template>
  <h2 :id="labelToId(label)" class="chat-title flex gap-2 items-center font-bold">
    <span>{{ num }}.</span>
    <img v-if="img" :src="img" :alt="`${aiName} logo`" class="h-4.5 w-4.5" />
    <UIcon v-if="icon" :name="icon" class="h-4.5 w-4.5" />
    <span>{{ aiName }}</span>
    <template v-if="platform == 'antigravity'">
      <span>via</span>
      <img src="/images/antigravity.svg" alt="Antigravity IDE" class="h-4.5" />
    </template>
    <span>:</span>
    <span>{{ label }}</span>
  </h2>
</template>
