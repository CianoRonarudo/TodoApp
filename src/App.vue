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
        <TodoForm :priorities="priorities" @add-todo="addTodo"></TodoForm>
        <!-- Liste des Todo -->
        <div class="w-[100%]">
          <div class="bg-white w-[100%] pb-10 pt-2 px-3 rounded-md">
            <TodoItem v-for="todo in todos" v-bind:key="todo.id" :todo="todo" @todo-change-status="todoChangeStatus(todo)"></TodoItem>
          </div>
        </div>
      </div>
    </div>
    
  </div>
</template>

<script setup>
import { reactive, ref } from 'vue';
import TodoItem from './components/TodoItem.vue';
import TodoForm from './components/TodoForm.vue';

const priorities = reactive([
  'High',
  'Low'
])

const todos = ref(
  [
    { id: 1, text: 'Learn', status: 'Active', priority: 'High', completed: false },
    { id: 2, text: 'Eat', status: 'Completed', priority: 'Low', completed: true },
    { id: 3, text: 'Play guitare', status: 'Active', priority: 'Low', completed: false }
  ]
)
const myTodo = ref('')
const isEdit = ref(null)
// const addTodo = () => {
//   if (isEdit.value === null) {
//     if (myTodo.value.length > 0) {
//       let newTodo = {
//         id: todos.value.length + 1,
//         text: myTodo.value,
//         status: 'Active',
//         priority: 'Low',
//         completed: false

//       }
//       todos.value.push(newTodo)
//     }
//   } else {
//     todos.value[isEdit.value].text = myTodo.value
//     isEdit.value = null
//   }


//   console.log("no task")
//   myTodo.value = ''


// }



// Nouvelles fonctions pour les fonctionnalités du TodoApp
const addTodo = (newTodo) => {
  let readyAddTodo = {
    id: todos.value.length,
    text: newTodo.text,
    status: 'Active',
    priority: newTodo.priority,
    completed : false
  }
  todos.value.push(readyAddTodo)
}



const deleteTodo = (index) => todos.value.splice(index - 1, 1)
const editTodo = (index) => {
  myTodo.value = todos.value[index - 1].text
  isEdit.value = index-1
  console.log(todos.value[index-1].text)
}

const todoChangeStatus = (todo) => {
  console.log(todo)
  todo.status = 'Active'
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
