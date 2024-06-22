<template>
    <form class="flex justify-between pb-10" @submit.prevent='addTodo'>
          <input v-model="newTodo.text" type="text" class="py-3 w-[60%] pl-5 rounded-full focus:outline-none focus:ring focus:border-blue-500" placeholder="Add a task ...">
          <select v-model="newTodo.priority" class="bg-white rounded-full px-2 w-[20%]">
            <option disabled value="">Choose a priority</option>
            <option v-for="priority in props.priorities" :value="priority">{{ priority }}</option>
            
          </select>
          <input type="submit" value="Add" class="px-6 bg-sky-500 text-white rounded-full w-[15%]">
    </form>
</template>

<script setup>
import { ref } from 'vue';
const newTodo = ref({
  text: '',
  priority: ''
})
const props = defineProps({
  priorities: {
    type: Object,
    required: true
  },
  
})
const emit = defineEmits([
  'add-todo'
])
function addTodo() {
  emit("add-todo", newTodo.value)
  newTodo.value.text = '',
  newTodo.value.priority = ''
}


</script>

<style scoped>

</style>