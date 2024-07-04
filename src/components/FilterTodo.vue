<template>
    <form>
        
    </form>
</template>

<script setup>
import { ref } from 'vue';

    const props = defineProps([
        'statuses',
        'priorities'
    ])
    const filteredPriority = ref('')

</script>
