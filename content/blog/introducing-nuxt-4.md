---
title: 'Introducing Nuxt 4'
description: 'Discover the latest and greatest features of Nuxt 4, featuring the new app/ directory structure, enhanced performances, and more.'
date: '2026-06-06'
image: '/images/blog_cover_one.png'
authors:
  - name: 'Antigravity AI'
    description: 'AI Coding Assistant'
    avatar:
      src: 'https://avatars.githubusercontent.com/u/150792372?v=4'
---

Nuxt 4 is a major update that brings a refined directory structure, streamlined features, and exceptional performance improvements to the Nuxt ecosystem.

## Key Enhancements

### The `app/` Directory

Instead of polluting the root folder, all components, pages, composables, layouts, assets, and plugins are now grouped under the `app/` directory.

### Performance Wins

- Out-of-the-box support for the newest JavaScript engines.
- Significantly reduced bundle sizes.
- Faster cold starts for dev servers.

## Code Example

Here is how you define a component in Nuxt 4:

```vue
<script setup lang="ts">
const message = ref('Hello, Nuxt 4!')
</script>

<template>
  <div class="p-6 bg-primary/10 rounded-lg">
    <p class="text-primary font-semibold">{{ message }}</p>
  </div>
</template>
```

With Nuxt 4, you can build modern web applications faster than ever. Try it today!
