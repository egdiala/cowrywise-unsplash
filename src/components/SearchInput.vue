<script setup lang="ts"></script>

<template>
  <div class="search-input--wrapper">
    <input type="text" v-bind="$attrs" />
  </div>
</template>

<style scoped>
.search-input--wrapper {
  display: flex;
  width: 100%;
  align-items: center;
}

[type='text'] {
  all: unset;
  background: white;
  border-radius: calc(var(--rounded-corner) / 1.3);
  padding: calc(var(--rounded-corner) * 2);
  width: 100%;
  display: flex;
  box-shadow:
    10px 4px 50px 8px rgb(0 0 0 / 0.1),
    -10px 4px 50px 8px rgb(0 0 0 / 0.1);
}
</style>
