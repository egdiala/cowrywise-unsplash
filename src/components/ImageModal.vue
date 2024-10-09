<script setup lang="ts">
import type { FetchedPhoto } from '@/types/photo'

defineProps<{ image: FetchedPhoto }>()
const modalEmits = defineEmits<{ (e: 'close'): void }>()
</script>

<template>
  <div class="modal" @click="modalEmits('close')">
    <div class="modal-container">
      <button type="button" class="close-btn" @click="modalEmits('close')">X</button>
      <div class="modal-content">
        <div class="image-container">
          <img :src="image.urls.regular" :alt="image.alt_description" class="modal-image" />
        </div>
        <div class="modal-details">
          <h4>{{ image.user.name }}</h4>
          <p>{{ image.user.location ?? '-' }}</p>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.modal {
  position: fixed;
  inset: 0;
  background-color: rgba(0, 0, 0, 0.8);
  display: flex;
  justify-content: center;
  align-items: center;
  z-index: 10;
  transition: opacity 0.3s;
  padding-left: 16px;
  padding-right: 16px;
}

.modal-image {
  transition: transform 0.3s ease;
  object-fit: cover;
  object-position: center;
  max-height: 691px;
  width: 100%;
}

.modal-container {
  display: flex;
  flex-direction: column;
  gap: 16px;
  margin-top: 20px;
  margin-bottom: 20px;
  overflow: hidden;
  width: max(1079px, 60%);
}

.close-btn {
  all: unset;
  font-weight: 500;
  font-size: 18px;
  color: white;
  width: fit-content;
  display: grid;
  place-content: center;
  margin-left: auto;
}

.modal-content {
  height: max(700px, 70%);
  overflow: hidden;
  background-color: white;
  display: flex;
  flex-direction: column;
  border-radius: calc(var(--rounded-corner) * 2);
}

.modal-details {
  padding: 12px 24px;
  display: grid;
  gap: 10px;

  h4 {
    color: #243c4f;
    font-size: 20px;
    font-weight: 600;
  }

  p {
    color: #828a8e;
    font-size: 14px;
    font-weight: 500;
  }
}

.image-container {
  height: min(500px, 40%);
  overflow: hidden;
}
</style>
