<script setup lang="ts">
import { onMounted, ref } from 'vue'
import ItemCard from './components/ItemCard.vue'

const page = ref<number>(1)

const characters = ref<Array<any>>([])

const getCards = async () => {
  const response = await (
    await fetch(`https://rickandmortyapi.com/api/character?page=${page.value}`)
  ).json()

  characters.value = response.results
}

const next = () => {
  page.value++
}

const prev = () => {
  page.value--
}

onMounted(async () => {
  await getCards()
})
</script>

<template>
  <div class="wrapper">
    <div class="container">
      <div class="content">
        <div class="cards-grid">
          <ul class="cards">
            <ItemCard
              v-for="character in characters"
              :key="character.id"
              :name="character.name"
              :location="character.location.name"
              :episode="character.episode"
              :image="character.image"
              :status="character.status"
              :species="character.species"
            />
          </ul>
        </div>
        <div class="pagination">
          <ul class="pagination__counts">
            <li class="pagination__count"></li>
          </ul>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped></style>
