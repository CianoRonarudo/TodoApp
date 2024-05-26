<template>
  <div class="lg:pt-20 h-full w-full bg-slate-800">
    <h1 class="text-3xl  text-white text-center font-bold">
      My TodoApp
    </h1>
    <div class="flex justify-center items-center flex-col">
      <div class="w-1/2 p-5 bg-slate-600">
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
      </div>
      <div class="pt-4 w-1/2">
        <form class="flex justify-between">
          <input type="text" class="py-3 w-[60%] pl-3 rounded-full focus:outline-none focus:ring focus:border-blue-500" placeholder="Add a task ...">
          <select class="bg-white rounded-full px-2 w-[20%]">
            <option>Low</option>
            <option>High</option>
          </select>
          <input type="submit" value="Add" class="px-6 bg-sky-500 text-white rounded-full w-[15%]">
        </form>
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
