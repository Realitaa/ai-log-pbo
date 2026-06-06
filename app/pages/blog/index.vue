<script setup lang="ts">
const { data: posts } = await useAsyncData('blog-posts', () =>
  queryCollection('blog').order('date', 'DESC').all(),
)

useSeoMeta({
  title: 'Blog - Nuxt Starter Template',
  description:
    'Stay up to date with the latest news and updates about Nuxt, web development, and AI tools.',
})
</script>

<template>
  <UContainer class="py-12 max-w-6xl">
    <UPageHero
      title="Latest Insights"
      description="Explore expert tutorials, deep dives, and announcements in modern web development."
      align="center"
    />

    <UPageBody class="mt-12">
      <UBlogPosts v-if="posts && posts.length">
        <UBlogPost
          v-for="(post, index) in posts"
          :key="index"
          v-bind="post"
          :to="post.path"
          variant="outline"
          class="transition-all duration-300 hover:shadow-xl hover:-translate-y-1"
        />
      </UBlogPosts>
      <div v-else class="text-center py-24 border border-dashed border-default rounded-xl">
        <UIcon name="i-lucide-newspaper" class="w-12 h-12 text-muted mx-auto mb-4" />
        <p class="text-toned font-medium text-lg">No articles published yet.</p>
        <p class="text-muted text-sm mt-1">Check back later for new content!</p>
      </div>
    </UPageBody>
  </UContainer>
</template>
