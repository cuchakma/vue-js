<script setup>
import {ref, onMounted} from 'vue';
    const name    = ref('John Doe');
    const status  = ref('active');
    const tasks   = ref(['Task One', 'Task Two', 'Task Three']);
    const newTask = ref('')

    const toggleStatus = () => {
        if( status.value == 'active' ) {
            status.value = 'pending';
        } else if( this.status == 'pending' ) {
            status.value = 'inactive';
        } else  {
            status.value = 'active';
        }
    }

    const addTask = () => {
        if( newTask.value.trim() != '' ) {
            tasks.value.push(newTask.value);
            newTask.value = '';
        }
    }

    const deleteTask = (taskId) => {
        let newTasks = tasks.value.filter((value, index) => {
            return index != taskId;
        });
        tasks.value = newTasks;
    }
    onMounted(async() =>{
        try {
            const response = await fetch('https://jsonplaceholder.typicode.com/todos');
            const data    = await response.json();
            tasks.value   = data.map((task) => (task.title));
        } catch {
            console.log('Error Fetching Task')
        }
    });
</script>

<template>

    <form @submit.prevent="addTask">
        <label for="newTask">Add Task</label>
        <input type="text" id="newTask" name="newTask" v-model="newTask"/>
        <button type="submit">Submit</button>
    </form>

    <h1 v-if="tasks?.length > 0">Task</h1>
    <ul v-if="tasks?.length > 0">
        <li v-for="(task, index) in tasks" :key="index">
            <span>{{ task }}</span>
            <button @click="deleteTask(index)">x</button>
        </li>
    </ul>

    <h1>{{ name }}</h1>
    <h3>{{ status }}</h3>
    <button @click="toggleStatus">Change Status</button>
</template>