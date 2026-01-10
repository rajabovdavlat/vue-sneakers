<script setup lang="ts">
import { inject } from 'vue'
import Card from './Card.vue'

interface Sneaker {
  id: number
  title: string
  imageUrl: string
  price: number
  isFavorite: boolean
}

const props = defineProps<{
  items: Sneaker[]
}>()

const addToFavorite = inject<(item: Sneaker) => void>('addToFavorite')!

const onClickAdd = () => {
  alert('Добавили в корзину!')
}

const handleFavorite = (item: Sneaker) => {
  addToFavorite(item)
}
</script>

<template>
  <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 xl:grid-cols-4 gap-8">
    <Card
      v-for="item in items"
      :key="item.id"
      :id="item.id"
      :imageUrl="item.imageUrl"
      :title="item.title"
      :price="item.price"
      :isFavorite="item.isFavorite"
      @clickAdd="onClickAdd"
      @clickFavorite="() => handleFavorite(item)" 
    />
  </div>
</template>