<script setup lang="ts">
const props = defineProps<{
  id: number
  title: string
  imageUrl: string
  price: number
  isFavorite: boolean
  isAdded: boolean
}>()

const emit = defineEmits<{
  clickFavorite: []
  clickAdd: []
}>()

const handleFavorite = () => {
  emit('clickFavorite')
}

const handleAdd = () => {
  emit('clickAdd')
}
</script>

<template>
  <div class="relative bg-white border border-slate-100 rounded-3xl p-8 cursor-pointer transition hover:-translate-y-2 hover:shadow-xl">
    <img
      @click="handleFavorite"
      :src="props.isFavorite ? '/like-2.svg' : '/like-1.svg'"
      alt="Избранное"
      class="absolute top-8 left-8 cursor-pointer"
    />
    <img :src="props.imageUrl" alt="Кроссовки" class="w-full" />
    <p class="mt-4">{{ props.title }}</p>

    <div class="flex justify-between items-center mt-6">
      <div class="flex flex-col">
        <span class="text-slate-400 text-sm">Цена:</span>
        <b class="text-xl">{{ props.price.toLocaleString('ru-RU') }} руб.</b>
      </div>
      <img
        @click="handleAdd"
        :src="props.isAdded ? '/checked.svg' : '/plus.svg'"
        alt="Добавить в корзину"
        class="cursor-pointer"
      />
    </div>
  </div>
</template>