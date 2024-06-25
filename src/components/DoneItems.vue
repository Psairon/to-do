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
            <input type="checkbox"  @change="() => emit('change', task)"  checked>
            <span>{{ task }}</span>
        </div>
            <button class="btn-remove" @click="() => emit('delite', task)">Delete</button>
    </li>
</template>