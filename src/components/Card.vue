<template>
  <div class="card">
    <div class="card-inner">
      <div class="card-content">
        {{ isTurned ? translate : text }}
      </div>
    </div>
    <div class="card-number">
      {{ number }}
    </div>
    <div v-if="status != undefined" class="status-icon">
      <svg
        v-if="status === false"
        width="24"
        height="24"
        viewBox="0 0 24 24"
        fill="none"
        xmlns="http://www.w3.org/2000/svg"
        :style="{ scale: 48 / 24 }"
      >
        <path
          fill-rule="evenodd"
          clip-rule="evenodd"
          d="M15.461 14.389L14.4 15.45L11.999 13.051L9.599 15.447L8.539 14.386L10.938 11.991L8.539 9.593L9.6 8.532L12 10.931L14.401 8.534L15.461 9.596L13.061 11.991L15.461 14.389ZM12 2.25C6.624 2.25 2.25 6.624 2.25 12C2.25 17.376 6.624 21.75 12 21.75C17.376 21.75 21.75 17.376 21.75 12C21.75 6.624 17.376 2.25 12 2.25Z"
          fill="#D00303"
        />
      </svg>
      <svg
        v-if="status === true"
        width="24"
        height="24"
        viewBox="0 0 24 24"
        fill="none"
        xmlns="http://www.w3.org/2000/svg"
        :style="{ scale: 48 / 24 }"
      >
        <path
          fill-rule="evenodd"
          clip-rule="evenodd"
          d="M12.4693 15.308L12.2543 15.689H11.4143L11.1613 15.353C11.1463 15.33 9.6593 13.108 7.7373 11.892L7.1023 11.492L7.9043 10.224L8.5373 10.624C9.92231 11.499 11.0723 12.777 11.7503 13.63C12.8153 12.025 15.3093 8.682 19.1343 5.971C17.3473 3.709 14.5863 2.25 11.4873 2.25C6.1113 2.25 1.7373 6.624 1.7373 12C1.7373 17.376 6.1113 21.75 11.4873 21.75C16.8633 21.75 21.2373 17.376 21.2373 12C21.2373 10.263 20.7753 8.635 19.9763 7.221C15.1433 10.667 12.4983 15.257 12.4693 15.308Z"
          fill="#09BB00"
        />
      </svg>
    </div>
    <button v-if="!isTurned" class="card-action" @click="turnOver">
      ПЕРЕВЕРНУТЬ
    </button>
    <div v-if="isTurned && status === undefined" class="card-turn-btn">
      <div @click="changeStatus(false)">
        <svg
          width="24"
          height="24"
          viewBox="0 0 24 24"
          fill="none"
          xmlns="http://www.w3.org/2000/svg"
        >
          <path
            fill-rule="evenodd"
            clip-rule="evenodd"
            d="M15.461 14.389L14.4 15.45L11.999 13.051L9.599 15.447L8.539 14.386L10.938 11.991L8.539 9.593L9.6 8.532L12 10.931L14.401 8.534L15.461 9.596L13.061 11.991L15.461 14.389ZM12 2.25C6.624 2.25 2.25 6.624 2.25 12C2.25 17.376 6.624 21.75 12 21.75C17.376 21.75 21.75 17.376 21.75 12C21.75 6.624 17.376 2.25 12 2.25Z"
            fill="#D00303"
          />
        </svg>
      </div>
      <div @click="changeStatus(true)">
        <svg
          width="24"
          height="24"
          viewBox="0 0 24 24"
          fill="none"
          xmlns="http://www.w3.org/2000/svg"
        >
          <path
            fill-rule="evenodd"
            clip-rule="evenodd"
            d="M12.4693 15.308L12.2543 15.689H11.4143L11.1613 15.353C11.1463 15.33 9.6593 13.108 7.7373 11.892L7.1023 11.492L7.9043 10.224L8.5373 10.624C9.92231 11.499 11.0723 12.777 11.7503 13.63C12.8153 12.025 15.3093 8.682 19.1343 5.971C17.3473 3.709 14.5863 2.25 11.4873 2.25C6.1113 2.25 1.7373 6.624 1.7373 12C1.7373 17.376 6.1113 21.75 11.4873 21.75C16.8633 21.75 21.2373 17.376 21.2373 12C21.2373 10.263 20.7753 8.635 19.9763 7.221C15.1433 10.667 12.4983 15.257 12.4693 15.308Z"
            fill="#09BB00"
          />
        </svg>
      </div>
    </div>
    <div v-else-if="isTurned" class="complete">ЗАВЕРШЕНО</div>
  </div>
</template>

<script setup>
import { ref } from "vue";

defineProps({
  number: {
    type: [String, Number],
    required: true,
  },
  text: {
    type: String,
    required: true,
  },
  translate: {
    type: String,
    required: true,
  },
});

const emit = defineEmits(["changeStatus", "turn"]);

const isTurned = ref(false);

const status = ref();

const turnOver = () => {
  isTurned.value = !isTurned.value;
  emit("turn", isTurned.value);
};

const changeStatus = (value) => {
  status.value = value;
  emit("changeStatus", value);
};
</script>

<style scoped>
.card {
  display: flex;
  width: 250px;
  height: 376px;
  position: relative;
  background: #ffffff;
  border-radius: 16px;
  justify-content: center;
  box-shadow: 0 8px 24px rgba(0, 0, 0, 0.08);
  cursor: pointer;
}

.card:hover {
  box-shadow: 0 16px 32px rgba(0, 0, 0, 0.12);
}

.card-inner {
  flex: 1;
  border: 1px solid #cce8ff;
  border-radius: 12px;
  margin: 28px 19px;
  flex-direction: column;
  align-items: center;
  display: flex;
}

.card-number {
  display: flex;
  flex-direction: row;
  position: absolute;
  top: 20px;
  left: 35px;
  font-size: 14px;
  color: #000;
  background-color: #fff;
  font-family: var(--font-family);
  font-weight: 400;
  font-size: 14px;
  text-align: center;
  color: #000;
}

.card-content {
  flex: 1;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 18px;
  color: #000;
}

.card-action {
  position: absolute;
  text-align: center;
  margin-bottom: 12px;
  background: #fff;
  border: none;
  font-size: 12px;
  letter-spacing: 0.08em;
  cursor: pointer;
  bottom: 8px;
  font-family: var(--font-family);
  font-weight: 700;
  font-size: 12px;
  line-height: 150%;
  letter-spacing: 0.12em;
  color: #222;
  display: flex;
}

.card-turn-btn {
  position: absolute;
  text-align: center;
  margin-bottom: 12px;
  background: #fff;
  border: none;
  font-size: 12px;
  letter-spacing: 0.08em;
  cursor: pointer;
  bottom: 1px;
  font-family: var(--font-family);
  font-weight: 700;
  font-size: 12px;
  line-height: 150%;
  letter-spacing: 0.12em;
  color: #222;
  display: flex;
  gap: 32px;
}

.complete {
  position: absolute;
  text-align: center;
  margin-bottom: 12px;
  background: #fff;
  border: none;
  font-size: 12px;
  letter-spacing: 0.08em;
  cursor: pointer;
  bottom: 8px;
  font-family: var(--font-family);
  font-weight: 700;
  font-size: 12px;
  line-height: 150%;
  letter-spacing: 0.12em;
  color: #222;
  display: flex;
}

.status-icon {
  position: absolute;
  margin-top: 16px;
  background: #fff;
}
</style>
