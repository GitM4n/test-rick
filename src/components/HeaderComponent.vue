<script setup lang="ts">
import IconFilter from "@/assets/icons/IconFilter.vue";
const emit = defineEmits<{
  (e: "open-modal"): void;
}>();
</script>

<template>
  <header class="header">
    <div class="container">
      <div class="header__inner">
        <h2 class="header__title">The Rick and Morty characters</h2>
        <IconFilter 
          class="header__filter" 
          @click="emit('open-modal')" 
        />
      </div>
    </div>
  </header>
</template>

<style scoped>
.header {
  background: rgb(241, 241, 241);
}

.header__inner {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  height: 400px;
}

.header__title {
  color: rgb(32, 35, 41);
  font-size: 8rem;
  text-wrap: balance;
  text-align: center;
  font-weight: 900;
}

.header__filter {
  width: 50px;
}

@media (max-width: 599px) {
  .header__title {
    font-size: 5rem;
  }
}
</style>
