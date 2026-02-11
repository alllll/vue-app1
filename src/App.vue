<script setup>
import { computed, reactive } from "vue";
import Button from "./components/Button.vue";
import Card from "./components/Card.vue";
import Score from "./components/Score.vue";

const cards = reactive([
  {
    word: "unadmitted",
    translation: "не допущенный",
    status: "pending",
  },
  {
    word: "unadmitted",
    translation: "не допущенный",
    status: "pending",
  },
  {
    word: "unadmitted",
    translation: "не допущенный",
    status: "pending",
  },
  {
    word: "unadmitted",
    translation: "не допущенный",
    status: "pending",
  },
]);

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
