<script setup></script>

<template>
  <button class="button">
    <slot />
  </button>
</template>

<style scoped>
.button {
  border: none;
  border-radius: 100px;
  background: var(--color-bg);
  padding: 16px 10px;
  font-family: var(--font);
  font-size: 24px;
  font-weight: 400;
  text-align: center;
  font-weight: 400;
  width: 335px;
  height: 68px;
  color: var(--color-primary);
  cursor: pointer;
}
</style>
