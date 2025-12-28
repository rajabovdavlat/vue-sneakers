<script setup lang="ts">
import Card from "./Card.vue";


const onClickAdd = () => {
  alert('Добавить!')
}
</script>

<template>
  <div class="grid grid-cols-4 gap-5">
    <Card
      imageUrl="/sneakers/sneakers-1.jpg"
      title="Мужские Кроссовки Nike Blazer Mid Suede"
      price="1280 руб."
     :isFavorite='false'
     :onClickAdd='onClickAdd'
    />
   
  </div>
</template>
