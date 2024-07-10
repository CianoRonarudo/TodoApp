<template>
    <div class="flex flex-col">
        <div class="text-indigo-400 font-bold text-xl mb-3">
            {{ title }}
        </div>
        <div>
            <form>
                <input :placeholder="title" type="text" class="py-2 rounded-full w-[60%] mr-3 px-5 border focus:outline-none focus:ring focus:ring-indigo-50 text-gray-600">
                <select name="" id="" class="w-1/3 rounded-full py-2 px-3 bg-white border text-gray-600 focus:outline-none focus:ring focus:ring-indigo-50">
                    <option value="">Priority</option>
                    <option value="High">High</option>
                    <option value="Low">Low</option>
                </select>
            </form>
        </div>
    </div>
</template>

<script setup>
const props = defineProps([
    'isAddForm',
])
console.log(props.isAddForm)
let title = props.isAddForm ? 'Ajouter un todo' : 'Editer un todo'


</script>

<style lang="scss" scoped>

</style>