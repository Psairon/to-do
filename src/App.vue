<script setup>
import { ref, watch } from 'vue';
import DoneItems from './components/DoneItems.vue';
import ToDoItems from './components/ToDoItems.vue';

let valueInput = ref('');
const needDoList = ref([]);
const completedList = ref([]);

const handlyInput = (event) => {
    valueInput.value = event.target.value;
}

const addTask = () => {
    if (valueInput.value === '') {
        return
    };
    needDoList.value.push({
        id: Math.random(),
        task: valueInput.value
    });
    valueInput.value = '';
}

const doChek = (task, type) => {
    if (type === 'need') {
        let id = needDoList.value.findIndex(item => item.task === task);
        const completedItem = needDoList.value.splice(id, 1);
        completedList.value.push(...completedItem);
    } else {
        let id = completedList.value.findIndex(item => item.task === task);
        const nocompletedItem = completedList.value.splice(id, 1);
        needDoList.value.push(...nocompletedItem);
    }
}

const deliteTask = (task, type) => {
    if (type === 'need') {
        let id = needDoList.value.findIndex(item => item.task === task);
        needDoList.value.splice(id, 1);
    } else {
        let id = completedList.value.findIndex(item => item.task === task);
        completedList.value.splice(id, 1);
    }
}

</script>

<template>
    <header>
        <h1>TO DO LIST</h1>
    </header>
    <div class="content">
        <div class="to-do">
            <div class="create-to-do">
                <input type="text" class="to-do-input" v-bind:value="valueInput" @input="handlyInput" @keypress.enter="addTask">
                <button class="createToDo" @click="addTask">add new task</button>
            </div>
            <div class="to-do-list">
                <h2>
                    <span>To Do</span>
                    <span class="mask-num">{{ needDoList.length }}</span>
                </h2>
                <ul class="mask-list">
                    <ToDoItems v-for="item in needDoList" :task="item.task" :index="item.id" :key="item.id" @change="doChek" @delite="deliteTask"/>
                </ul>
                <h2>
                    <span>Done!</span>
                    <span class="mask-num">{{ completedList.length }}</span>
                </h2>
                <ul class="mask-list completed">
                    <DoneItems  v-for="item in completedList" :task="item.task" :key="item.id" :index="item.id" @change="doChek" @delite="deliteTask"/>
                </ul>
            </div>
        </div>
        <div class="aesthetic">
            <div style="margin-top: 15px;">
                <img src="/src/assets/4.jpg" alt="">
                <div class="audio">
                    <img src="/src/assets/audio.jpg" alt="">
                </div>
                <img src="/src/assets/9.jpg" alt="">
                <img src="/src/assets/12.jpg" alt="">
            </div>
            <div>
                <img src="/src/assets/5.jpg" alt="">
                <img src="/src/assets/1.jpg" alt="">
                <img src="/src/assets/7.jpg" alt="">
            </div>
        </div>
    </div>
</template>

