<script setup>
import Button from "./components/Button.vue";
import Card from "./components/Card.vue";
import Score from "./components/Score.vue";
</script>

<template>
  <header class="header">
    <div class="header-title">ЗАПОМНИ СЛОВО</div>
    <Score />
  </header>
  <main class="main">
    <Card number="01" word="unadmitted" translation="не допущенный" />

    <Button>Начать игру</Button>
  </main>
</template>

<style scoped>
.header {
  display: flex;
  justify-content: space-between;
  align-items: center;
}
.main {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  min-height: 100vh;

  text-align: center;
}

.header-title {
  font-family: var(--font-family);
  font-weight: 700;
  font-size: 16px;
  line-height: 150%;
  letter-spacing: 0.12em;
  color: #222;
}
</style>
