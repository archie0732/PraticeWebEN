<template>
  <div class="container mx-auto px-4 py-8">
    <div class="max-w-2xl mx-auto">
      <h2 class="text-3xl font-bold text-center mb-8">單字練習</h2>
      <div v-if="currentWord" class="bg-white rounded-lg shadow-lg p-6">
        <div class="mb-6">
          <img
            :src="currentWord.imageUrl || '/api/placeholder/400/300'"
            :alt="currentWord.english"
            class="w-full h-48 object-cover rounded mb-4"
          />
          <p class="text-2xl font-bold text-center mb-4">{{ currentWord.english }}</p>
        </div>
        <div class="grid grid-cols-2 gap-4">
          <button
            v-for="option in options"
            :key="option"
            @click="checkAnswer(option)"
            class="bg-gray-100 hover:bg-gray-200 text-gray-800 font-semibold py-2 px-4 rounded"
          >
            {{ option }}
          </button>
        </div>
        <div v-if="showResult" class="mt-4 text-center">
          <p :class="isCorrect ? 'text-green-600' : 'text-red-600'" class="text-xl font-bold">
            {{ isCorrect ? "答對了！" : "答錯了！" }}
          </p>
          <button
            @click="nextQuestion"
            class="mt-4 bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded"
          >
            下一題
          </button>
        </div>
      </div>
      <div v-else class="text-center">
        <p class="text-xl">暫無單字可供練習，請先新增單字！</p>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref, onMounted } from "vue";
import type { Word } from "@/types/word";

const words = ref<Word[]>([]);
const currentWord = ref<Word | null>(null);
const options = ref<string[]>([]);
const showResult = ref<boolean>(false);
const isCorrect = ref<boolean>(false);

const loadWords = (): void => {
  words.value = JSON.parse(localStorage.getItem("words") || "[]");
  if (words.value.length > 0) {
    nextQuestion();
  }
};

const generateOptions = (correct: string): string[] => {
  const allOptions = words.value.map((w) => w.chinese).filter((c) => c !== correct);
  const shuffled = allOptions.sort(() => 0.5 - Math.random());
  const wrongOptions = shuffled.slice(0, 3);
  return [...wrongOptions, correct].sort(() => 0.5 - Math.random());
};

const nextQuestion = (): void => {
  showResult.value = false;
  const randomIndex = Math.floor(Math.random() * words.value.length);
  currentWord.value = words.value[randomIndex];
  if (currentWord.value) {
    options.value = generateOptions(currentWord.value.chinese);
  }
};

const checkAnswer = (selected: string): void => {
  showResult.value = true;
  isCorrect.value = selected === currentWord.value?.chinese;
};

onMounted(() => {
  loadWords();
});
</script>
