<script setup>

const props = defineProps({
    index: Number,
    task: String,
})

const emit = defineEmits(['change', 'delite'])

</script>

<template>
    <li>
        <div class="to-do-item">
            <input type="checkbox" @change="() => emit('change', task, 'need')" >
            <span> {{ task }}</span>
        </div>
        <button class="btn-remove" @click="() => emit('delite', task, 'need')">Delete</button>
    </li>
</template>