<script setup lang="ts">
defineProps({
  name: {
    type: String,
    required: true,
  },
  icon: {
    type: String,
    required: true,
  },
})

const iconMap: Record<string, string> = {
  pdf: 'material-icon-theme:pdf',
}
</script>

<template>
  <div class="bg-white p-4 rounded-lg flex gap-4 items-center">
    <UIcon :name="iconMap[icon]" class="size-10" />
    <p class="font-medium">{{ name }}</p>
  </div>
</template>