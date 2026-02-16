<script setup>
import { computed, reactive, ref } from "vue";

import Button from "./components/Button.vue";
import Card from "./components/Card.vue";
import Score from "./components/Score.vue";
import Spinner from "./components/Spinner.vue";

const isLoading = ref(false);
const cards = reactive([]);

const startGame = async () => {
  // Reset cards before fetching new ones
  cards.splice(0);
  isLoading.value = true;
  try {
    const res = await fetch("http://localhost:8080/api/random-words");
    if (!res.ok) throw new Error(`HTTP error ${res.status}`);
    const data = await res.json();
    cards.push(
      ...data.map((c, i) => ({ ...c, status: "pending", number: i + 1 })),
    );
    isLoading.value = false;
  } catch (e) {
    console.error("Failed to load words:", e);
    isLoading.value = false;
  }
};

const score = computed(() => {
  return cards.reduce((acc, item) => {
    if (item.status === "success") return acc + 10;
    if (item.status === "fail") return acc - 4;
    return acc;
  }, 0);
});
</script>

<template>
  <header class="header">
    <div class="header-title">ЗАПОМНИ СЛОВО</div>
    <Score :count="score" />
  </header>
  <main class="main">
    <Spinner v-if="isLoading" />
    <template v-else>
      <div class="btn-wrapper">
        <Button v-if="cards.length === 0" @click="startGame"
          >Начать игру</Button
        >
      </div>

      <Card
        v-for="(card, index) in cards"
        :key="index"
        :number="card.number"
        :word="card.word"
        :translation="card.translation"
        :status="card.status"
        @change-status="
          (status) => {
            cards[index].status = status;
          }
        "
      />
      <div class="btn-wrapper">
        <Button v-if="cards.length > 0" @click="startGame"
          >Начать заново</Button
        >
      </div>
    </template>
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
.btn-wrapper {
  display: flex;
  justify-content: center;
  grid-column: 1 / -1;
  margin-top: 16px;
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
