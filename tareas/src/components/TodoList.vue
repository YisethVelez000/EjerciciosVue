<template>
    <form id="app" @submit.prevent="createTask" >
        <label class="label" for="task">Nueva tarea:</label>
        <input type="text" v-model="newTask" id="task" />
        <input type="submit" value="Crear tarea" />
    </form>
    <ul>
        <li v-for="(task, i) in tasks" :key="'task' + i" :class="{ completed: task.completed }">
            <input type="checkbox" @change="completeTask(task.text)" :checked="task.completed" />
            {{ task.text }}
        </li>
    </ul>
</template>

<script>
export default {
    data: () => ({
        newTask: "",
        tasks: [],
    }),
    methods: {
        createTask() {
            let task = {
                text: this.newTask,
                completed: true,
            };
            this.tasks.push(task);
            this.newTask = "";
            console.log(this.tasks);
        },
        completeTask(taskText) {
            for (let i = 0; i < this.tasks.length; i++) {
                let task = this.tasks[i];
                if (taskText === task.text) {
                    task.completed = !task.completed;
                }
            }
        },
    },
};
</script>
<style scoped>
.completed {
    text-decoration: line-through;
    color: rgb(154, 201, 255);
}
</style>