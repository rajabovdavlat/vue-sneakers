<script setup lang="ts">
import Header from "./components/Header.vue";
import CardList from "./components/CardList.vue";
import Drawer from "./components/Drawer.vue";
</script>

<template>
  <!-- <Drawer /> -->
  <div class="bg-white w-4/5 m-auto rounded-xl shadow-xl mt-14">
    <Header />

    <div class="p-10">
      <div class="flex justify-between">
        <h2 class="text-3xl font-bold mb-8">Все крассовок</h2>

        <div class='relative'>
          <img class="absolute left-4 top-3 " src="/search.svg" alt="Search" />
          <input
            class="border border-gray-300 rounded-lg py-2 pl-10 pr-4 outline-none focus:border-slate-400"
            type="text"
            placeholder="Поиск..."
          />
        </div>
      </div>

      <CardList />
    </div>
  </div>
</template>

<style scoped>
/* Можно оставить пустым или добавить свои стили */
</style>
