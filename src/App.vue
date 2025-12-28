<script setup>
import Header from "./components/Header.vue";
</script>

<template>
  <div class="bg-white w-4/5 m-auto h-screen rounded-xl shadow-xl mt-14">
    <Header />

    <div class="">
      <div class='relative m-10 border border-slate-100 rounded-3xl p-8 cursor-pointer transition hover:-translate-y-2 hover:shadow-xl'>
        <img src="/like-2.svg" alt="Like 2" class='absolute  top-8 left-8' />
        <img src="/sneakers/sneakers-1.jpg" alt="Sneaker" />
        <p class='mt-2'>Мужские Кроссовки Nike Blazer Mid Suede</p>
        <div class="flex justify-between">
          <div class='flex flex-col mt-5'>
            <span class='text-slate-400'>Цена:</span>
            <b>1205 руб.</b>
          </div>
          <img src="/plus.svg" alt="Plus">
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
/* Можно оставить пустым или добавить свои стили */
</style>
