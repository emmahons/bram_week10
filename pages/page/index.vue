<template>
  <div>
    <div class="pr-5">
      <Drawer />
    </div>
    <main class="mx-auto max-w-4xl space-y-6 px-4 mb-20">
      <div class="text-3xl font-bold">
        Work
      </div>
      <!-- Responsive Masonry Layout -->
      <div class="masonry space-x-8">
        <div class="masonry-item" v-for="post in posts" :key="post.slug">
          <div class="masonry-image ">
            <NuxtImg :src="post.thumbnail" alt="Post thumbnail" class="w-full h-64 object-cover  mb-2"
              :width="750" :height="550" />
          </div>
          <NuxtLink :to="post._path" class="block">
            <div class="masonry-item-text mb-12">
              <h2 class="text-xl font-semibold mb-2 text-black">{{ post.title }}</h2>
              <!-- Limiting the height of the description and making it responsive -->
              <p v-if="post.description" class="text-gray-600 line-clamp-3 ">{{ post.description }}</p>
              <ClientOnly>
                <article v-if="post.tags" class="text-xs mt-2 text-black">
                  <li v-for="(item, index) in post.tags" :key="index" class="inline mr-2 text-black">
                    <NuxtLink :to="`/tags/${item}`">{{ item }}</NuxtLink>
                  </li>
                </article>
              </ClientOnly>
            </div>
          </NuxtLink>



        </div>
      </div>
    </main>
  </div>
</template>

<script setup>
const { data: posts } = await useAsyncData('posts', () => {
  return queryContent('/page')
    .sort({ promoted: 1 })

    .find()
})
</script>