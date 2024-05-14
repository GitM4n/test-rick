<script setup lang="ts">
import { onMounted, ref } from 'vue'

const props = defineProps<{
  name: string
  location: string
  species: string
  episode: string
  image: string
  status: string
}>()

const episodeName = ref<string>('')

const getEpisodeName = async () => {
  const result = await (await fetch(props.episode)).json()
  episodeName.value = result.name || 'Unknown'
}

onMounted(async () => {
  await getEpisodeName()
})
</script>

<template>
  <li class="card">
    <div class="card__inner character">
      <div class="character__image">
        <img :src="props.image" alt="avatar" />
      </div>
      <div class="character__content">
        <h3 class="character__name">{{ props.name }}</h3>
        <div class="character__status-species">
          <div
            class="indicator"
            :style="{
              backgroundColor: status === 'Alive' ? 'green' : status === 'unknown' ? 'gray' : 'red'
            }"
          ></div>
          <p class="status">{{ props.status }}</p>
          -
          <p class="species">{{ props.species }}</p>
        </div>
        <div class="character__location">
          <p>Last known location:</p>
          <p>{{ props.location }}</p>
        </div>
        <div class="character__episode">
          <p>First seen in</p>
          <p>{{ episodeName }}</p>
        </div>
      </div>
    </div>
  </li>
</template>

<style scoped>
.card {
  list-style: none;
}

.character {
  display: flex;
  color: white;
}

.character__name {
  font-size: 24px;
  font-weight: 900;
}

.indicator {
  width: 10px;
  height: 10px;
  border-radius: 50%;
}

.character__status-species {
  display: flex;
  align-items: center;
  gap: 5px;
}

.character__status-species p {
  font-size: 18px;
  font-weight: 700;
}

.character__location,
.character__episode {
  display: flex;
  flex-direction: column;
}

.character__location p:first-child,
.character__episode p:first-child {
  font-weight: 700;
  color: gray;
}
</style>
