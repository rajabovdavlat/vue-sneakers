<script setup lang="ts">
import { onMounted, provide, reactive, ref, watch } from 'vue'
import axios from 'axios'
import Header from './components/Header.vue'
import CardList from './components/CardList.vue'
// import Drawer from './components/Drawer.vue'

interface Sneaker {
  id: number
  title: string
  imageUrl: string
  price: number
  isFavorite?: boolean
  favoriteId?: number  // ID записи в favorites
  isAdded?: boolean
}

const items = ref<Sneaker[]>([])

const filters = reactive({
  sortBy: 'title' as string,
  searchQuery: '',
})

const onChangeSelect = (event: Event) => {
  const target = event.target as HTMLSelectElement
  filters.sortBy = target.value
}

const fetchItems = async () => {
  try {
    const params: Record<string, string> = {
      sortBy: filters.sortBy,
    }

    if (filters.searchQuery) {
      params.title = `*${filters.searchQuery}*`
    }

    const { data } = await axios.get<Sneaker[]>(
      'https://de8fff53e0466791.mokky.dev/items',
      { params }
    )

    // Добавляем дефолтные поля
    items.value = data.map(item => ({
      ...item,
      isFavorite: false,
      isAdded: false,
    }))
  } catch (err) {
    console.error('Ошибка загрузки товаров:', err)
  }
}

const fetchFavorites = async () => {
  try {
    const { data: favorites } = await axios.get<any[]>(
      'https://de8fff53e0466791.mokky.dev/favorites'
    )

    items.value = items.value.map(item => {
      const favorite = favorites.find(f => f.parentId === item.id)
      if (favorite) {
        return {
          ...item,
          isFavorite: true,
          favoriteId: favorite.id
        }
      }
      return item
    })
  } catch (err) {
    console.error('Ошибка загрузки избранного:', err)
  }
}

const addToFavorite = async (item: Sneaker) => {
  if (item.isFavorite) {
    // Удалить из избранного
    try {
      await axios.delete(`https://de8fff53e0466791.mokky.dev/favorites/${item.favoriteId}`)
      item.isFavorite = false
      item.favoriteId = undefined
    } catch (err) {
      console.error('Ошибка удаления из избранного:', err)
    }
  } else {
    // Добавить в избранное
    try {
      const { data } = await axios.post('https://de8fff53e0466791.mokky.dev/favorites', {
        parentId: item.id,
      })
      item.isFavorite = true
      item.favoriteId = data.id
    } catch (err) {
      console.error('Ошибка добавления в избранное:', err)
    }
  }
}

onMounted(async () => {
  await fetchItems()
  await fetchFavorites()
})

watch(filters, fetchItems, { deep: true })

provide('addToFavorite', addToFavorite)
</script>

<template>
  <!-- <Drawer /> -->
  <div class="w-4/5 mx-auto mt-14 rounded-xl bg-white shadow-xl">
    <Header />

    <div class="p-10">
      <div class="flex justify-between items-center mb-8">
        <h2 class="text-3xl font-bold">Все кроссовки</h2>

        <div class="flex gap-4 items-center">
          <select
            @change="onChangeSelect"
            class="py-2 px-3 rounded-lg outline-none border border-gray-300 shadow-lg"
          >
            <option value="title">По названию</option>
            <option value="price">По цене (дешевле)</option>
            <option value="-price">По цене (дороже)</option>
          </select>

          <div class="relative">
            <img class="absolute left-4 top-3 w-5" src="/search.svg" alt="Поиск" />
            <input
              v-model="filters.searchQuery"
              class="border shadow-lg border-gray-300 rounded-lg py-2 pl-10 pr-4 outline-none focus:border-slate-400 w-64"
              type="text"
              placeholder="Поиск..."
            />
          </div>
        </div>
      </div>

      <CardList :items="items" />
    </div>
  </div>
</template>

<style scoped>
/* Опционально */
</style>