<script setup lang="ts">
import type { FetchedPhoto } from '@/types/photo'
import { reactive, ref } from 'vue'
import ImageModal from './ImageModal.vue'

defineProps<{ image: FetchedPhoto }>()

const isOpen = ref(false)

const toggleModal = (e?: MouseEvent) => {
  if (document.startViewTransition) {
    document.startViewTransition(() => {
      isOpen.value = !isOpen.value
    })
  } else {
    isOpen.value = !isOpen.value
  }
}
</script>

<template>
  <div class="image-card--container" @click="(e) => toggleModal(e)">
    <img
      :src="image.urls.small"
      :alt="image.alt_description"
      :srcset="Object.values(image.urls).join(',')"
    />
    <div
      class="image-card--details"
      :class="reactive({ 'image-card--tint': image.color.startsWith('#f') })"
    >
      <h4>{{ image.user.name }}</h4>
      <p>{{ image.user.location ?? '-' }}</p>
    </div>
  </div>
  <ImageModal v-if="isOpen" :image="image" @close="toggleModal" />
</template>

<style scoped>
.image-card--container {
  border-radius: var(--rounded-corner);
  height: fit-content;
  overflow: hidden;
  position: relative;
}

.image-card--container img {
  width: 100%;
  display: block;
  object-fit: cover;
}

img:hover {
  transform: scale(1.05);
}

.image-card--details {
  position: absolute;
  inset: 0;
  display: flex;
  flex-direction: column;
  justify-content: end;
  color: var(--vt-c-white);
  padding: calc(var(--rounded-corner) * 2);

  h4 {
    font-size: 18px;
    filter: none;
    color: white;
  }

  p {
    font-size: 14px;
  }
}

.image-card--tint {
  background: linear-gradient(180deg, transparent 50%, rgba(22, 24, 21, 1) 100%);
}
</style>
