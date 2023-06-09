<script setup lang="ts">
import { computed, ref } from 'vue'

interface Task {
    name: string
    complete: boolean
}

const tasks = ref<Task[]>([
    { name: 'ToDolist作成', complete: true },
    { name: 'なろう講習会', complete: false },
])

const newTaskName = ref('')

const addTask = () => {
    tasks.value.push({
        name: newTaskName.value,
        complete: false,
    })
    newTaskName.value = ''
}

const completed = computed(() => tasks.value.filter((task) => task.complete))
const uncompleted = computed(() => tasks.value.filter((task) => !task.complete))

</script>

<template>
    <div>
        <div>ToDoList</div>
        <ul>
            <li v-for="task in completed" :key="task.name">
                    <div>{{ task.name }}</div>
                    <div :class="{ completed: true }">完了</div>
            </li>
            <li v-for="task in uncompleted" :key="task.name">
                    <div>{{ task.name }}</div>
                    <div v-if="task.complete == false" :class="{ unconpleted: true }">
                        未完了
                        <button @click="task.complete = true">終わった！</button>
                    </div>
            </li>
        </ul>
        <div>
            <label>
                名前：
                <input v-model="newTaskName" type="text" />
            </label>
            <button @click="addTask">追加</button>
        </div>
    </div>
</template>

<style>
.unconpleted {
    color: red;
}

.completed {
    color: greenyellow;
}
</style>