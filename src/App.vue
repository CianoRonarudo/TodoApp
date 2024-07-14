

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
        <input v-model="search" @input="handleSearchTodo" type="text" class="w-[89%] py-3 rounded-full px-5" placeholder="Rechercher une todo ...">
        <button @click="showSearchInput" class="w-[10%] rounded-full flex items-center justify-center bg-indigo-600 text-white">
          <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="size-8">
            <path stroke-linecap="round" stroke-linejoin="round" d="M6 18 18 6M6 6l12 12" />
          </svg>

        </button>
      </div>
      <div>
        <input required v-model="data" class="py-3 rounded-full mt-10 mb-10 pr-5 pl-7 w-full" type="text" :placeholder="isEditTodo ? 'Modifier le todo' : 'Ajouter le todo'" @keyup.enter="addTodo">
      </div>
      <div class="bg-white mt-5 w-[100%] pb-10 pt-2 px-3 rounded-xl text-slate-600">
        <TodoItem v-if="shownTodos.length > 0" v-for="todo in shownTodos" 
          :todo="todo" v-bind:key="todo.id"
          @handle-click-on-edit-button="handleClikOnEditButton(todo)"
          @handle-click-on-delete-button="handleClickOnDeleteButton(todo)"
          @change-todo-priority="changeTodoPriority(todo)"
        >
        </TodoItem>
        <div v-else class="flex justify-center items-center text-slate-400">
          Aucun todo disponible
        </div>

        <!-- Boutton d'ajout de Todo -->
        <div class="pt-2 flex justify-end pb-1">
          <span class="bg-indigo-600 shadow-lg cursor-pointer rounded-full font-bold text-xl text-white" @click="handleClickOnAddTodoButton">
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
import { computed, ref } from 'vue'
const search = ref('')
//constitution d'une base de données 
const todos = ref([
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

])

const clickTodo = ref({})
  

const filteredTodos = {
  all: (todos) => todos,
  active: (todos) => todos.filter((todo) => !todo.completed),
  completed: (todos) => todos.filter((todo) => todo.completed),
  search: (todos) => {
    if (search.value === '') {
      return todos
    }
    else {
      const searchQuery = search.value.toLowerCase()
      return todos.filter((todo) => todo.name.toLowerCase().includes(searchQuery))
    }
  } 
}
const visibility = ref('all')

const shownTodos = computed(() => {
  return filteredTodos[visibility.value](todos.value)
})

const filterFunction = (tag) => {
  visibility.value = tag
}

// Variable et fonction pour le truc de recherche
const visibleSearchInput = ref(false)
const showSearchInput = () =>
  visibleSearchInput.value = !visibleSearchInput.value

// edit Todo
const isEditTodo = ref(false)
// Ajout de todo
const data = ref('')
const addTodo = () => {
  if (data.value !== '') {
    if (!isEditTodo.value) {
      const maxId = todos.value.reduce((max, todo) => Math.max(max, todo.id), 0)
      console.log(maxId)
      todos.value.push(
        {
          id: maxId + 1,
          name: data.value,
          completed: false,
          priority: 'Low'
        }
      )
    }
    else {
      todos.value[findTodoIndexById(clickTodo.value.id)].name = data.value
      isEditTodo.value = false
    }
    data.value = ''
  }
} 
const findTodoIndexById = (id) => {
  return todos.value.findIndex(todo => todo.id === id)
}

const handleClikOnEditButton = (todo) => {
  clickTodo.value = { ...todo }
  // console.log(clickTodo.value)
  // console.log(todos.value[findTodoIndexById(clickTodo.value.id)])
  data.value = todos.value[findTodoIndexById(clickTodo.value.id)].name
  isEditTodo.value = true
  // console.log(todos.value)
}

const handleClickOnDeleteButton = (todo) => {
  clickTodo.value = { ...todo}
  todos.value = todos.value.filter((todo) => todo.id !== clickTodo.value.id)
  
}

const handleSearchTodo = () => {
  filterFunction('search')
  console.log('Recherche ,', search.value)

}

const changeTodoPriority = (todo) => {
  clickTodo.value = { ...todo}
  todos.value[findTodoIndexById(clickTodo.value.id)].priority = todos.value[findTodoIndexById(clickTodo.value.id)].priority === 'Low' ? 'High' : 'Low'
}
</script>

