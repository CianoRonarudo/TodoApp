

<template>
  <div class="h-screen bg-slate-800 flex justify-center">
    <div class="w-1/3 pt-8">
      <div class="text-white font-bold text-3xl text-center">
        TodoApp
      </div>
      <div @click="showSearchInput" v-show="!visibleSearchInput" class="mt-2 pt-2 cursor-pointer hover:text-white flex h-[56px] items-center text-slate-400 font-semibold text-lg">
        <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="size-6">
          <path stroke-linecap="round" stroke-linejoin="round" d="m21 21-5.197-5.197m0 0A7.5 7.5 0 1 0 5.196 5.196a7.5 7.5 0 0 0 10.607 10.607Z" />
        </svg>
        <span class="pl-3">Rechercher une todo ...</span>
      </div>
      <div v-show="visibleSearchInput" class="w-full flex justify-between mt-2 pt-2">
        <input type="text" class="w-[89%] py-3 rounded-full px-5" placeholder="Rechercher une todo ...">
        <button @click="showSearchInput" class="w-[10%] rounded-full flex items-center justify-center bg-indigo-600 text-white">
          <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="size-8">
            <path stroke-linecap="round" stroke-linejoin="round" d="M6 18 18 6M6 6l12 12" />
          </svg>

        </button>
      </div>
      <div class="bg-white mt-5 w-[100%] pb-10 pt-2 px-3 rounded-xl text-slate-600">
        <TodoItem v-if="shownTodos.length > 0" v-for="todo in shownTodos" :todo="todo" v-bind:key="todo.id"></TodoItem>
        <div v-else class="flex justify-center items-center text-slate-400">
          Aucun todo disponible
        </div>
        <div class="pt-2 flex justify-end pb-1">
          <span class="bg-indigo-600 shadow-lg rounded-full font-bold text-xl text-white">
            <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="size-5">
              <path stroke-linecap="round" stroke-linejoin="round" d="M12 4.5v15m7.5-7.5h-15" />
            </svg>

          </span>
        </div>
        <div class="flex justify-center items-center">
          <div class="w-1/2 flex justify-between">
            <button @click="filterFunction('all')" class="py-1 px-2 rounded-lg hover:bg-indigo-100 active:bg-indigo-200 focus:outline-none focus:ring focus:ring-indigo-300">
              All
            </button>
          <button @click="filterFunction('active')" class="py-1 px-2 rounded-lg hover:bg-indigo-100 active:bg-indigo-200 focus:outline-none focus:ring focus:ring-indigo-300">
            Active
          </button>
          <button @click="filterFunction('completed')" class="py-1 px-2 rounded-lg hover:bg-indigo-100 active:bg-indigo-200 focus:outline-none focus:ring focus:ring-indigo-300">
            Completed
          </button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import TodoItem from '@/components/TodoItem.vue'
import { computed, ref } from 'vue';

//constitution d'une base de données 
const todos = [
  {
    id: 1,
    name: 'Learn',
    completed: true,
    priority : 'High'
  },
  {
    id: 2,
    name: 'Eat',
    completed: false,
    priority : 'Low'
  },
  {
    id: 3,
    name: 'Pray',
    completed: true,
    priority : 'High'
  },

]

const filteredTodos = {
  all: (todos) => todos,
  active: (todos) => todos.filter((todo) => !todo.completed),
  completed: (todos) => todos.filter((todo) => todo.completed),
}
const visibility = ref('all')

const shownTodos = computed(() => filteredTodos[visibility.value](todos))

const filterFunction = (tag) => {
  visibility.value = tag
}


// Variable et fonction pour le truc de recherche
const visibleSearchInput = ref(false)
const showSearchInput = () =>
  visibleSearchInput.value = !visibleSearchInput.value

</script>

