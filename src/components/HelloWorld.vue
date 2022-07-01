<!--data and logic-->
<script setup>

    import { ref } from 'vue'

    let tasks = ref([]) // interface Task { id: number, title: string, description, date: Date, completed: false }

    let task = ref({
        id: tasks.length,
        title: '',
        description: '',
        dueDate: '',
        completed: false
    })

    const createTask = () => {
        tasks.value.push(task.value)
        task.value = {
            id: tasks.length,
            title: '',
            description: '',
            dueDate: '',
            completed: false
        }
    }

    const updateTask = (t) => {
        tasks.value[t.id] = t
    }

    const deleteTask = (t) => {
        tasks.value.splice(t.id, 1)
    }

</script>

<!--ui component-->
<template>

    <div class="todo-list">

        <div>
            <h1>Create Task</h1>
            <input type="text" v-model="task.title">
            <input type="text" v-model="task.description">
            <input type="date" v-model="task.dueDate">
            <button @click="createTask">Create</button>
        </div>


        <div>
            <h1>Todo List</h1>
            <div v-if="tasks.every(t => t.completed === true)">Create a task to display your todo list.</div>

            <div class="tasks" v-for="t in tasks" >
                <div class="task" v-if="t.completed === false">
                    <input type="text" v-model="t.title">
                    <input type="text" v-model="t.description">
                    <input type="date" v-model="t.dueDate">
                    <input type="checkbox" v-model="t.completed">
                    <button @click="updateTask(t)">Update</button>
                    <button @click="deleteTask(t)">Delete</button>
                </div>
            </div>
        </div>

        <div>
            <h1>Completed Tasks</h1>
            <div v-if="tasks.every(t => t.completed === false)">Complete a task to display your completed tasks.</div>

            <div class="tasks" v-for="t in tasks" >
                <div class="task" v-if="t.completed === true">
                    <input type="text" v-model="t.title">
                    <input type="text" v-model="t.description">
                    <input type="date" v-model="t.dueDate">
                    <input type="checkbox" v-model="t.completed">
                    <button @click="updateTask(t)">Update</button>
                    <button @click="deleteTask(t)">Delete</button>
                </div>
            </div>
        </div>

    </div>

</template>

<!--ui styles-->
<!--scoped applies styles only to the parent component while no scoped also applies styles to child components-->
<style scoped>
</style>
