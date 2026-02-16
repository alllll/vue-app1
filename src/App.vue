<script setup>
import { computed, onMounted, reactive } from "vue";
import Button from "./components/Button.vue";
import Card from "./components/Card.vue";
import Score from "./components/Score.vue";

const cards = reactive([]);

/* eslint-disable-next-line no-undef */
onMounted(async () => {
  try {
    const res = await fetch("http://localhost:8080/api/random-words");
    if (!res.ok) throw new Error(`HTTP error ${res.status}`);
    const data = await res.json();
    // ensure each card has status
    cards.push(
      ...data.map((c, i) => ({ ...c, status: "pending", number: i + 1 })),
    );
  } catch (e) {
    console.error("Failed to load words:", e);
  }
});

const balance = computed(() => {
  return cards.filter((item) => item.status === "success").length;
});
</script>

<template>
  <header class="header">
    <div class="header-title">ЗАПОМНИ СЛОВО</div>
    <Score :count="balance" />
  </header>
  <main class="main">
    <Card
      v-for="(card, index) in cards"
      :key="index"
      :number="card.number"
      :word="card.word"
      :translation="card.translation"
      @change-status="
        (status) => {
          cards[index].status = status;
        }
      "
    />

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
  display: grid;
  grid-template-columns: repeat(5, 1fr);
  gap: 16px;
  justify-content: center;
  align-items: start;
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
