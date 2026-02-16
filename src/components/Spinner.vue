<template>
  <div class="spinner"></div>
</template>

<script setup></script>

<style scoped>
.spinner {
  width: 48px;
  height: 48px;
  border: 4px solid #ccc;
  border-top-color: #333;
  border-radius: 50%;
  animation: spin 1s linear infinite;
}

@keyframes spin {
  to { transform: rotate(360deg); }
}
</style>
