<script setup lang="ts">
import { onMounted, ref } from 'vue'
import ItemCard from './components/ItemCard.vue'
import HeaderComponent from './components/HeaderComponent.vue';
import LoaderComponent from './components/LoaderComponent.vue';
import PaginationComponent from './components/PaginationComponent.vue';
import ModalComponent from './components/ModalComponent.vue';
import type { ICharacter } from './interfaces';

const loadingCards = ref<boolean>(true)
const currentPage = ref<number>(1)

const characters = ref<ICharacter[]>([])
const totalPages = ref<number[]>([])

const isModal = ref<boolean>(false)

const nameFilter = ref<string>('')
const statusFilter = ref<string>('')



const getCards = async () => {

  let name = nameFilter.value
  let status = statusFilter.value

  name === '' ? name = '' : name = `name=${name}`
  status === 'any' ? status = '' : status = `status=${status}`

  loadingCards.value = true
  document.body.classList.add('lock')

  const res = await fetch(`https://rickandmortyapi.com/api/character/?page=${currentPage.value}&${name}&${status}`)
  
  if(res.ok){
    const result = await res.json()
    characters.value = result.results
    await generatePagesArr(result.info.pages)
    
  }else{
      console.log('error:' + res.status)
      characters.value = []
  }
  
  setTimeout(() => {
    loadingCards.value = false
    document.body.classList.remove('lock')
    window.scrollTo({ top: 400, behavior: 'smooth' })
  }, 2000)
 

}

const updatePage = async(page:number) => {
  currentPage.value = page
  await getCards()

}

const generatePagesArr = async(length:number) => {
  
  totalPages.value = []
  for (let i = 1; i <= length; i++) {
    totalPages.value.push(i)
  }

}

const reset = async() => {
  currentPage.value = 1
  nameFilter.value = ''
  statusFilter.value = 'any'
  isModal.value = false
  await getCards()
}

const setFilters = async (name:string, status:string) => {
  currentPage.value = 1
  nameFilter.value = name
  statusFilter.value = status
  isModal.value = false
  await getCards()
}

onMounted(async () => {
  await getCards()

})
</script>

<template>
  <div class="wrapper">
    <HeaderComponent @open-modal="isModal=true" />
      <div class="content">
        <div class="container">
          <div class="cards-grid">
            <ul class="cards">
              <li class="no-result" v-if="characters.length === 0">No search results <span style="color:orange; cursor:pointer" @click="reset()">reload</span></li>
              <ItemCard
                v-for="character in characters"
                :key="character.id"
                :character="character"
              />
            </ul>
          </div>
          <div class="pagination">
            <PaginationComponent v-if="characters.length > 0" :pages-arr="totalPages" :current-page="currentPage" @update="updatePage"  />
          </div>
      </div>
      <ModalComponent @click="isModal=false" :is-open="isModal" @submit="setFilters"/>
    </div>
  <LoaderComponent v-show="loadingCards"/>
  </div>
</template>

<style>



.container{
  max-width: 1460px;
  padding: 0 15px;
  margin: 0 auto;
 
}

.content{
  color: white;
  padding: 40px 0;
}


.cards{
  display: grid;
  justify-content: center;
  grid-gap: 20px;
  grid-template-columns: repeat(auto-fit, minmax(450px, 600px));
  grid-template-rows: repeat(auto-fit, minmax(150px, 1fr));

}

.no-result{
  text-align: center;
  font-size: 2rem;
  font-weight: 900;
}

@media (max-width:599px){
  .cards{
    grid-template-columns: 1fr;
  }
}



</style>
