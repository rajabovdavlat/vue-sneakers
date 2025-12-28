<script setup lang="ts">
defineProps<{
  title: string;
  imageUrl: string;
  price: number;
  isFavorite: boolean;
  isAdded: boolean;
  onClickAdd: Function
  onClickFavorite: Function

}>();


</script>

<template>
  <div
    class="relative bg-white border border-slate-100 rounded-3xl p-8 cursor-pointer transition hover:-translate-y-2 hover:shadow-xl"
  >
    <img
      :src="!isFavorite ? '/like-1.svg' : '/like-2.svg'"
      alt="Like 2"
      class="absolute top-8 left-8"
      @click='onClickFavorite'
    />
    <img :src="imageUrl" alt="Sneaker" />
    <p class="mt-2">{{ title }}</p>
    <div class="flex justify-between">
      <div class="flex flex-col mt-5">
        <span class="text-slate-400">Цена:</span>
        <b>{{ price }}</b>
      </div>
      <img @click='onClickAdd' :src="!isAdded ? '/plus.svg' : '/checked.svg'" alt="Plus" />
    </div>
  </div>
</template>
