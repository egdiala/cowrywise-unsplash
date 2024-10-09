<script setup lang="ts"></script>

<template>
  <div class="skeleton-container">
    <div class="content content-1"></div>
    <div class="content content-2"></div>
  </div>
</template>

<style scoped>
.skeleton-container {
  position: relative;
  display: flex;
  flex-direction: column;
  justify-content: end;
  gap: 20px;
  height: 375px;
  overflow: hidden;
  border-radius: var(--rounded-corner);
  background-color: var(--vt-c-light-gray);
  padding: 1rem;
  box-shadow: var(--vt-ring-offset-shadow, 0 0 #0000), var(--vt-ring-shadow, 0 0 #0000),
    var(--vt-shadow);
}

.content {
  background-color: var(--vt-c-gray);
  padding: var(--rounded-corner);
  border-radius: calc(var(--rounded-corner) / 2);
}

.content-1 {
  width: 50%;
}

.content-2 {
  width: 25%;
}

@keyframes shimmer {
  0% {
    background-position: 100% 0;
  }
  100% {
    background-position: -100% 0;
  }
}

.skeleton-container::before {
  content: '';
  position: absolute;
  inset: 0;
  background: linear-gradient(
    90deg,
    rgba(231, 231, 231, 0) 0%,
    rgba(231, 231, 231, 0.3) 50%,
    rgba(231, 231, 231, 0) 100%
  );
  background-size: 200% 100%;
  animation: shimmer 1.5s infinite;
}
</style>
