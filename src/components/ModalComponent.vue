<script setup lang="ts">
import { ref, computed } from "vue";
import { characterNames } from "@/characterNames";

const props = defineProps<{
  isOpen: boolean;
}>();
const emit = defineEmits<{
  (e: "submit", name: string, status: string): void;
}>();

const currentName = ref<string>("");
const statusOptions = ["any", "alive", "dead", "unknown"];
const currentStatus = ref<string>(statusOptions[0]);
const filteredNames = computed(() => {
  return characterNames.value.filter((name) =>
    name.toLowerCase().startsWith(currentName.value.toLowerCase())
  );
});

const openName = ref<boolean>(false);
const setName = (name: string) => {
  currentName.value = name;
  openName.value = false;
};

const openStatus = ref<boolean>(false);
const setStatus = (status: string) => {
  currentStatus.value = status;
  openStatus.value = false;
};
</script>

<template>
  <div 
    class="modal" 
    :class="{ active: props.isOpen }"
    >
    <div 
      class="modal__inner" 
      @click.stop
      >
      <div class="modal__inputs">
        <div class="input__name">
          <label for="name">Имя персонажа</label>
          <input 
            id="name" 
            v-model="currentName"
            type="text"  
            @input="openName = true" 
          />
          <ul 
            v-if="openName && currentName.length > 0"
            class="name-options" 
            >
            <li 
              class="name-option" 
              @click="setName(currentName)"
            >
              {{ currentName }}
            </li>
            <li
              v-for="name in filteredNames"
              :key="name"
              class="name-option"
              @click="setName(name)"
            >
              {{ name }}
            </li>
          </ul>
        </div>

        <div class="input__status">
          <p for="status">Статус персонажа</p>
          <div class="input__status_content">
            <p
              class="current-status"
              :style="{
                backgroundColor:
                  currentStatus === 'alive'
                    ? 'green'
                    : currentStatus === 'dead'
                    ? 'red'
                    : 'gray',
              }"
              @click="openStatus = true"
            >
              {{ currentStatus }}
            </p>
            <ul 
              v-if="openStatus" 
              class="status-options" 
              >
              <li
                v-for="status in statusOptions"
                :key="status"
                class="status-option"
                @click="setStatus(status)"
              >
                {{ status }}
              </li>
            </ul>
          </div>
        </div>
      </div>
      <button 
        class="modal__submit" 
        @click="emit('submit', currentName, currentStatus)"
      >
        Применить
      </button>
      <button 
        class="modal__reset" 
        @click="emit('submit', '', 'any')"
      >
        Сброс
      </button>
    </div>
  </div>
</template>

<style scoped>
.modal {
  position: fixed;
  top: -200%;
  left: 0;
  right: 0;
  background: rgba(0, 0, 0, 0.5);
  transition: all 0.2s ease-in-out;
}

.modal.active {
  top: 0;
  bottom: 0;
}

.modal__inner {
  position: relative;
  background: rgb(39, 43, 51);
  height: 500px;
  border: 3px solid white;
  border-radius: 10px;
  padding: 1em;
  max-width: 600px;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  display: flex;
  flex-direction: column;
  gap: 10px;
  justify-content: center;
  align-items: center;
}

.modal__inputs {
  flex: 0 0 80%;
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 150px;
}

.input__name {
  position: relative;
  max-width: 300px;
}

input {
  width: 100%;
  appearance: none;
  border: none;
  outline: none;
  border-bottom: 0.2em solid gray;
  background: transparent;
  border-radius: 0.2em 0.2em 0 0;
  padding: 0.4em;
  color: white;
  transition: all 0.2s ease-in-out;
  font-size: 2rem;
}
input:focus {
  border-bottom: 0.2em solid white;
}

.name-options {
  position: absolute;
  width: 100%;
  height: 150px;
  overflow: auto;
  display: flex;
  flex-direction: column;
  gap: 10px;
  background: rgb(39, 43, 51);
  border-radius: 5px;
  border: 1px solid white;
}

.name-option,
.status-option,
.current-status {
  cursor: pointer;
  padding: 0 5px;
  font-size: 2rem;
}

.current-status {
  cursor: pointer;
  text-align: center;
  border-radius: 5px;
}
.input__status_content {
  position: relative;
  border-radius: 5px;
  background: gray;
  transition: all 0.2s ease-in-out;
}

.status-options {
  position: absolute;
  background: rgb(39, 43, 51);
  border-radius: 5px;
  border: 1px solid white;
  width: 100%;
}
.status-option {
  border-bottom: 1px solid black;
}

.modal__submit,
.modal__reset {
  appearance: none;
  border: none;
  outline: none;
  background: rgb(39, 43, 51);
  color: white;
  padding: 5px 10px;
  border-radius: 5px;
  font-size: 2rem;
  cursor: pointer;
}

.modal__submit:hover {
  background: rgb(60, 62, 68);
}

.modal__reset:hover {
  background: rgba(255, 58, 58, 0.575);
}
</style>
