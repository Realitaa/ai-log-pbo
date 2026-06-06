<script setup lang="ts">
const route = useRoute()

const { data: post } = await useAsyncData(route.path, () =>
  queryCollection('blog').path(route.path).first(),
)

if (!post.value) {
  throw createError({ statusCode: 404, statusMessage: 'Post not found', fatal: true })
}

useSeoMeta({
  title: () => `${post.value?.title || 'Blog Post'}`,
  description: () => post.value?.description || '',
})
</script>

<template>
  <UContainer class="py-12 print:py-0 print:ml-4 max-w-4xl">
    <!-- Back button -->
    <UButton
      to="/blog"
      icon="i-lucide-arrow-left"
      color="neutral"
      variant="ghost"
      class="mb-8 print:hidden"
      label="Back to Blog"
    />

    <article v-if="post">
      <!-- Title & Description -->
      <header class="mb-8 print:hidden">
        <h1 class="text-4xl font-extrabold tracking-tight text-highlighted sm:text-5xl mb-4">
          {{ post.title }}
        </h1>
        <p class="text-xl text-muted leading-8">
          {{ post.description }}
        </p>

        <!-- Metadata / Authors -->
        <div class="mt-6 flex flex-wrap items-center gap-6 pt-6 border-t border-default">
          <div v-if="post.authors && post.authors.length" class="flex items-center gap-3">
            <UAvatar
              v-for="(author, idx) in post.authors"
              :key="idx"
              :src="author.avatar?.src"
              :alt="author.name"
              size="md"
            />
            <div>
              <p class="text-sm font-semibold text-highlighted">
                {{ post.authors.map((a) => a.name).join(', ') }}
              </p>
              <p class="text-xs text-muted">
                {{ post.authors[0]?.description || 'Author' }}
              </p>
            </div>
          </div>

          <div class="text-sm text-muted">
            <time :datetime="post.date">{{
              new Date(post.date).toLocaleDateString('en-US', { dateStyle: 'long' })
            }}</time>
          </div>
        </div>
      </header>

      <!-- Cover Image -->
      <div
        v-if="post.image"
        class="mb-10 aspect-21/9 w-full overflow-hidden rounded-xl border border-default shadow-md"
      >
        <img :src="post.image" :alt="post.title" class="object-cover w-full h-full" />
      </div>

      <!-- Rendered Markdown Content -->
      <UPageBody class="prose dark:prose-invert max-w-none">
        <ContentRenderer :value="post" />
      </UPageBody>
    </article>
  </UContainer>
</template>
