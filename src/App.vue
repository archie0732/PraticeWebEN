<template>
  <div class="min-h-screen bg-gray-100">
    <nav class="bg-white shadow-lg">
      <div class="max-w-6xl mx-auto px-4">
        <div class="flex justify-between">
          <div class="flex space-x-7">
            <router-link to="/" class="flex items-center py-4 px-2">
              <span class="font-semibold text-gray-500 text-lg">英文學習</span>
            </router-link>
          </div>
          <div class="flex items-center space-x-3">
            <router-link to="/" class="py-4 px-2 text-gray-500 hover:text-green-500 transition duration-300"
              >首頁</router-link
            >
            <router-link to="/add" class="py-4 px-2 text-gray-500 hover:text-green-500 transition duration-300"
              >新增單字</router-link
            >
            <router-link to="/practice" class="py-4 px-2 text-gray-500 hover:text-green-500 transition duration-300"
              >單字練習</router-link
            >
            <router-link to="/daily" class="py-4 px-2 text-gray-500 hover:text-green-500 transition duration-300"
              >今日單字</router-link
            >
          </div>
        </div>
      </div>
    </nav>
    <router-view></router-view>
  </div>
</template>

<script setup lang="ts">
import { RouterLink, RouterView } from "vue-router";
</script>
