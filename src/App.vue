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
      <div class="flex justify-between items-center">
        <h2 class="text-3xl font-bold mb-8">Все крассовок</h2>


        <select class='py-2 px-3 rounded-md outline-none border border-gray-300 shadow-lg' name="" id="">
          <option>По названию</option>
          <option>По цене (дешевые)</option>
          <option>По цене (дорогие)</option>
        </select>
        <div class='relative'>
          <img class="absolute left-4 top-3 " src="/search.svg" alt="Search" />
          <input
            class="border shadow-lg border-gray-300 rounded-lg py-2 pl-10 pr-4 outline-none focus:border-slate-400"
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
