<script setup lang="ts">
import { ref, watch } from 'vue'
import { useFetch } from '@vueuse/core'
import ImageCard from '@/components/ImageCard.vue'
import SearchInput from '@/components/SearchInput.vue'
import type { FetchedPhoto } from '@/types/photo'

const url = ref(
  'https://api.unsplash.com/photos?client_id=PnRrOFHVJsrq50fUd-ratbz_JfA5cn_662OfCqBB19g'
)

const { data, isFetching } = useFetch<FetchedPhoto[]>(url).get().json()

const columns = ref<Array<FetchedPhoto[]>>([[], [], []])

const distributeImages = () => {
  columns.value = [[], [], []] // Reset the columns

  data.value?.forEach((image: FetchedPhoto, index: number) => {
    const columnIndex = index % 3 // Determine which column (0, 1, or 2)
    columns.value[columnIndex].push(image) // Push image into the right column
  })
}

watch(isFetching, () => {
  if (!isFetching.value) {
    distributeImages()
  }
})
</script>

<template>
  <main class="main">
    <header>
      <div class="container">
        <SearchInput placeholder="Search for image" />
      </div>
    </header>

    <div class="container">
      <div v-if="!isFetching" class="masonry-layout">
        <div class="masonry-column" v-for="(column, index) in columns" :key="index">
          <ImageCard v-for="image in column" :key="image.id" :image="image" />
        </div>
      </div>
    </div>
  </main>
</template>

<style scoped>
.main {
  display: flex;
  flex-direction: column;
  width: 100%;
}

header {
  display: flex;
  justify-items: center;
  align-items: center;
  background-color: var(--vt-c-light-blue);
}

@media (min-width: 1024px) {
  header {
    padding-top: 32px;
    padding-bottom: 32px;
  }

  .masonry-layout {
    gap: 64px;
  }
}

@media (min-width: 1536px) {
  header {
    padding-top: 64px;
    padding-bottom: 64px;
  }

  .masonry-layout {
    margin-top: -72px;
  }
}

.masonry-layout {
  display: flex;
  padding-left: 32px;
  padding-right: 32px;
}

@media (max-width: 640px) {
  .masonry-layout {
    flex-direction: column;
    gap: 16px;
    padding-left: 0px;
    padding-right: 0px;
  }
}

@media (min-width: 640px) {
  .masonry-layout {
    gap: 16px;
  }
}

.masonry-column {
  flex: 1;
  display: flex;
  flex-direction: column;
  gap: 16px;
}
</style>
