<template>
  <!-- Div de la page -->
  <div class="lg:pt-20 h-full w-full bg-slate-800">
    <!-- Titre de la page -->
    <h1 class="text-3xl  text-white text-center font-bold">
      My TodoApp
    </h1>
    <!-- Div de la liste -->

    <div class="flex justify-center items-center flex-col">
      <!-- Ancienne interface -->
      <!-- <div class="w-1/2 p-5 bg-slate-600">
        <div class="flex items-center justify-between w-full">
          <input
            class="focus: border border-slate-300 w-2/3 placeholder:text-slate-400 placeholder:italic shadow-sm rounded-md outline-none"
            placeholder="Enter your task ..." v-model="myTodo">
          <button @click="addTodo" class="w-1/4 shadow-sm rounded-sm bg-sky-400 text-white">Submit</button>
        </div>
        <div class="overflow-auto rounded-lg shadow">
          <table class="w-full">
            <thead class="bg-gray-50 border-b-2 border-gray-200">
              <tr>
                <th class="p-3 text-sm font-semibold tracking-wide text-left"></th>
                <th class="p-3 text-sm font-semibold tracking-wide text-left">Name</th>
                <th class="p-3 text-sm font-semibold tracking-wide text-left">Status</th>
                <th class="p-3 text-sm font-semibold tracking-wide text-left">Priority</th>
                <th class="p-3 text-sm font-semibold tracking-wide text-left">#</th>
                <th class="p-3 text-sm font-semibold tracking-wide text-left">#</th>
              </tr>
            </thead>
            <tbody class="divide-y divide-gray-100">

              <TodoItem v-for="todo in todos" v-bind:key="todo.id" :todo="todo" @edit-todo="editTodo(todo.id)" @delete-todo="deleteTodo(todo.id)" @todo-change-status="todoChangeStatus(todo.id)" @todo-change-priority="todoChangePriority(todo.id)"></TodoItem>

            </tbody>
          </table>
        </div>
      </div> -->
      <!-- Nouvelle interface pour l'app -->
      <div class="pt-4 w-1/2">
        <!-- Formulaire d'ajout d'une Todo -->
        <form class="flex justify-between pb-10">
          <input type="text" class="py-3 w-[60%] pl-5 rounded-full focus:outline-none focus:ring focus:border-blue-500" placeholder="Add a task ...">
          <select class="bg-white rounded-full px-2 w-[20%]">
            <option>Low</option>
            <option>High</option>
          </select>
          <input type="submit" value="Add" class="px-6 bg-sky-500 text-white rounded-full w-[15%]">
        </form>
        <!-- Liste des Todo -->
        <div class="w-[100%]">
          <div class="bg-white w-[100%] pb-10 pt-2 px-3 rounded-md">
            <!-- Une Todo -->
            <div class="border-b grid grid-cols-12 py-2">
              <div class="col-span-1 flex justify-center items-center">
                <input type="checkbox">
              </div>
              <div class="px-4 col-span-5 flex items-center">
                Visiter le musée
              </div>
              <div class="col-span-2 flex justify-center items-center">
                <!-- <span class="bg-sky-500 px-2 py-1 rounded-lg text-white text-xs uppercase" >Active</span> -->
                <span class="text-yellow-800 bg-yellow-200 rounded-lg bg-opacity-50 px-2 py-1 text-xs uppercase" >Completed</span>
              </div>
              <div class="col-span-2 flex justify-center items-center">
                <span class="bg-red-500 px-2 py-1 rounded-lg text-white text-xs font-bold uppercase">
                  Hight
                </span>
                <!-- <span class="bg-green-500 px-2 py-1 rounded-lg text-white text-xs font-bold uppercase">
                  Low
                </span> -->

              </div>
              <span class="col-span-1 flex justify-center items-center">
                <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="currentColor" class="w-4 h-4 hover:text-sky-600">
                  <path d="M21.731 2.269a2.625 2.625 0 0 0-3.712 0l-1.157 1.157 3.712 3.712 1.157-1.157a2.625 2.625 0 0 0 0-3.712ZM19.513 8.199l-3.712-3.712-12.15 12.15a5.25 5.25 0 0 0-1.32 2.214l-.8 2.685a.75.75 0 0 0 .933.933l2.685-.8a5.25 5.25 0 0 0 2.214-1.32L19.513 8.2Z" />
                </svg>
              </span>
              <span class="col-span-1 flex justify-center items-center">
                <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="w-4 h-4 hover:text-red-500">
                  <path stroke-linecap="round" stroke-linejoin="round" d="m14.74 9-.346 9m-4.788 0L9.26 9m9.968-3.21c.342.052.682.107 1.022.166m-1.022-.165L18.16 19.673a2.25 2.25 0 0 1-2.244 2.077H8.084a2.25 2.25 0 0 1-2.244-2.077L4.772 5.79m14.456 0a48.108 48.108 0 0 0-3.478-.397m-12 .562c.34-.059.68-.114 1.022-.165m0 0a48.11 48.11 0 0 1 3.478-.397m7.5 0v-.916c0-1.18-.91-2.164-2.09-2.201a51.964 51.964 0 0 0-3.32 0c-1.18.037-2.09 1.022-2.09 2.201v.916m7.5 0a48.667 48.667 0 0 0-7.5 0" />
                </svg>
              </span>
            </div>
            <!-- une todo -->
            <div class="border-b grid grid-cols-12 py-2">
              <div class="col-span-1 flex justify-center items-center">
                <input type="checkbox">
              </div>
              <div class="px-4 col-span-5 flex items-center">
                Visiter le musée
              </div>
              <div class="col-span-2 flex justify-center items-center">
                <span class="bg-sky-500 px-2 py-1 rounded-lg text-white text-xs uppercase" >Active</span>
                <!-- <span class="text-yellow-800 bg-yellow-200 rounded-lg bg-opacity-50 px-2 py-1 text-xs uppercase" >Completed</span> -->
              </div>
              <div class="col-span-2 flex justify-center items-center">
                <span class="bg-red-500 px-2 py-1 rounded-lg text-white text-xs font-bold uppercase">
                  Hight
                </span>
                <!-- <span class="bg-green-500 px-2 py-1 rounded-lg text-white text-xs font-bold uppercase">
                  Low
                </span> -->

              </div>
              <span class="col-span-1 flex justify-center items-center">
                <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="currentColor" class="w-4 h-4 hover:text-sky-600">
                  <path d="M21.731 2.269a2.625 2.625 0 0 0-3.712 0l-1.157 1.157 3.712 3.712 1.157-1.157a2.625 2.625 0 0 0 0-3.712ZM19.513 8.199l-3.712-3.712-12.15 12.15a5.25 5.25 0 0 0-1.32 2.214l-.8 2.685a.75.75 0 0 0 .933.933l2.685-.8a5.25 5.25 0 0 0 2.214-1.32L19.513 8.2Z" />
                </svg>
              </span>
              <span class="col-span-1 flex justify-center items-center">
                <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="w-4 h-4 hover:text-red-500">
                  <path stroke-linecap="round" stroke-linejoin="round" d="m14.74 9-.346 9m-4.788 0L9.26 9m9.968-3.21c.342.052.682.107 1.022.166m-1.022-.165L18.16 19.673a2.25 2.25 0 0 1-2.244 2.077H8.084a2.25 2.25 0 0 1-2.244-2.077L4.772 5.79m14.456 0a48.108 48.108 0 0 0-3.478-.397m-12 .562c.34-.059.68-.114 1.022-.165m0 0a48.11 48.11 0 0 1 3.478-.397m7.5 0v-.916c0-1.18-.91-2.164-2.09-2.201a51.964 51.964 0 0 0-3.32 0c-1.18.037-2.09 1.022-2.09 2.201v.916m7.5 0a48.667 48.667 0 0 0-7.5 0" />
                </svg>
              </span>
            </div>
            <!-- une todo -->
            <div class="border-b grid grid-cols-12 py-2">
              <div class="col-span-1 flex justify-center items-center">
                <input type="checkbox">
              </div>
              <div class="px-4 col-span-5 flex items-center">
                Visiter le musée
              </div>
              <div class="col-span-2 flex justify-center items-center">
                <span class="bg-sky-500 px-2 py-1 rounded-lg text-white text-xs uppercase" >Active</span>
                <!-- <span class="text-yellow-800 bg-yellow-200 rounded-lg bg-opacity-50 px-2 py-1 text-xs uppercase" >Completed</span> -->
              </div>
              <div class="col-span-2 flex justify-center items-center">
                <!-- <span class="bg-red-500 px-2 py-1 rounded-lg text-white text-xs font-bold uppercase">
                  Hight
                </span> -->
                <span class="bg-green-500 px-2 py-1 rounded-lg text-white text-xs font-bold uppercase">
                  Low
                </span>

              </div>
              <span class="col-span-1 flex justify-center items-center">
                <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="currentColor" class="w-4 h-4 hover:text-sky-600">
                  <path d="M21.731 2.269a2.625 2.625 0 0 0-3.712 0l-1.157 1.157 3.712 3.712 1.157-1.157a2.625 2.625 0 0 0 0-3.712ZM19.513 8.199l-3.712-3.712-12.15 12.15a5.25 5.25 0 0 0-1.32 2.214l-.8 2.685a.75.75 0 0 0 .933.933l2.685-.8a5.25 5.25 0 0 0 2.214-1.32L19.513 8.2Z" />
                </svg>
              </span>
              <span class="col-span-1 flex justify-center items-center">
                <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="w-4 h-4 hover:text-red-500">
                  <path stroke-linecap="round" stroke-linejoin="round" d="m14.74 9-.346 9m-4.788 0L9.26 9m9.968-3.21c.342.052.682.107 1.022.166m-1.022-.165L18.16 19.673a2.25 2.25 0 0 1-2.244 2.077H8.084a2.25 2.25 0 0 1-2.244-2.077L4.772 5.79m14.456 0a48.108 48.108 0 0 0-3.478-.397m-12 .562c.34-.059.68-.114 1.022-.165m0 0a48.11 48.11 0 0 1 3.478-.397m7.5 0v-.916c0-1.18-.91-2.164-2.09-2.201a51.964 51.964 0 0 0-3.32 0c-1.18.037-2.09 1.022-2.09 2.201v.916m7.5 0a48.667 48.667 0 0 0-7.5 0" />
                </svg>
              </span>
            </div>
            <!-- une todo -->
            <div class="border-b grid grid-cols-12 py-2">
              <div class="col-span-1 flex justify-center items-center">
                <input type="checkbox">
              </div>
              <div class="px-4 col-span-5 flex items-center">
                Visiter le musée
              </div>
              <div class="col-span-2 flex justify-center items-center">
                <!-- <span class="bg-sky-500 px-2 py-1 rounded-lg text-white text-xs uppercase" >Active</span> -->
                <span class="text-yellow-800 bg-yellow-200 rounded-lg bg-opacity-50 px-2 py-1 text-xs uppercase" >Completed</span>
              </div>
              <div class="col-span-2 flex justify-center items-center">
                <!-- <span class="bg-red-500 px-2 py-1 rounded-lg text-white text-xs font-bold uppercase">
                  Hight
                </span> -->
                <span class="bg-green-500 px-2 py-1 rounded-lg text-white text-xs font-bold uppercase">
                  Low
                </span>

              </div>
              <span class="col-span-1 flex justify-center items-center">
                <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="currentColor" class="w-4 h-4 hover:text-sky-600">
                  <path d="M21.731 2.269a2.625 2.625 0 0 0-3.712 0l-1.157 1.157 3.712 3.712 1.157-1.157a2.625 2.625 0 0 0 0-3.712ZM19.513 8.199l-3.712-3.712-12.15 12.15a5.25 5.25 0 0 0-1.32 2.214l-.8 2.685a.75.75 0 0 0 .933.933l2.685-.8a5.25 5.25 0 0 0 2.214-1.32L19.513 8.2Z" />
                </svg>
              </span>
              <span class="col-span-1 flex justify-center items-center">
                <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="w-4 h-4 hover:text-red-500">
                  <path stroke-linecap="round" stroke-linejoin="round" d="m14.74 9-.346 9m-4.788 0L9.26 9m9.968-3.21c.342.052.682.107 1.022.166m-1.022-.165L18.16 19.673a2.25 2.25 0 0 1-2.244 2.077H8.084a2.25 2.25 0 0 1-2.244-2.077L4.772 5.79m14.456 0a48.108 48.108 0 0 0-3.478-.397m-12 .562c.34-.059.68-.114 1.022-.165m0 0a48.11 48.11 0 0 1 3.478-.397m7.5 0v-.916c0-1.18-.91-2.164-2.09-2.201a51.964 51.964 0 0 0-3.32 0c-1.18.037-2.09 1.022-2.09 2.201v.916m7.5 0a48.667 48.667 0 0 0-7.5 0" />
                </svg>
              </span>
            </div>
          </div>
        </div>
      </div>
    </div>
    
  </div>
</template>

<script setup>
import { reactive, ref } from 'vue';
import TodoItem from './components/TodoItem.vue';

const todos = ref(
  [
    { id: 1, text: 'Learn', status: 'Active', priority: 'Hight', completed: false },
    { id: 2, text: 'Eat', status: 'Completed', priority: 'Low', completed: true },
    { id: 3, text: 'Play guitare', status: 'Active', priority: 'Low', completed: false }
  ]
)
const myTodo = ref('')
const isEdit = ref(null)
const addTodo = () => {
  if (isEdit.value === null) {
    if (myTodo.value.length > 0) {
      let newTodo = {
        id: todos.value.length + 1,
        text: myTodo.value,
        status: 'Active',
        priority: 'Low',
        completed: false

      }
      todos.value.push(newTodo)
    }
  } else {
    todos.value[isEdit.value].text = myTodo.value
    isEdit.value = null
  }

  
  console.log("no task")
  myTodo.value = ''


}
const deleteTodo = (index) => todos.value.splice(index - 1, 1)
const editTodo = (index) => {
  myTodo.value = todos.value[index - 1].text
  isEdit.value = index-1
  console.log(todos.value[index-1].text)
}

const todoChangeStatus = (index) => {
  todos.value[index - 1].completed = !todos.value[index - 1].completed
  todos.value[index - 1].status = todos.value[index - 1].completed ? "Completed" : "Active"
}
const todoChangePriority = (index) => {
  if (todos.value[index - 1].priority ==="Low") {
    todos.value[index - 1].priority = "High"
  }
  else {
    todos.value[index - 1].priority = "Low"
  }
}
</script>

<style scoped>

</style>
