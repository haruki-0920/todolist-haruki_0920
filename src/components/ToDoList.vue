<script setup lang="ts">
import { ref } from 'vue'
interface Task {
    name: string
}

const tasks = ref<Task[]>([
])

const newTaskName = ref('')

const addItem = () => {
    if (
        tasks.value.some(
            task => task.name === newTaskName.value            
        )
    ) {
        return
    }
    if (newTaskName.value === '') {
        return
    } 
    tasks.value.push({name: newTaskName.value})

    newTaskName.value = ''
}

const deleteTask = (name: string) => {
    tasks.value = tasks.value.filter(
        task => task.name !== name
    )
}
</script>

<template>
    <div>
        <div>TaskList</div>
        <ul>
            
            <li v-for = "task in tasks" :key = "task.name">
                <div>名前: {{ task.name }}</div>
                <button @click = "deleteTask(task.name)">削除</button>                
            </li>
        </ul>
        <div>
            <label>
                名前
                <!-- synchronize the input field with the variable -->
                <input v-model = "newTaskName" type = "text" />
            </label>
            <button @click = "addItem">追加</button>
        </div>

    </div>
</template>
<!--
タスクは未完または完了済みの状態を持つ。
タスクはタスク名を持つ。
未完タスクのリストと完了済みタスクのリストが表示される。
タスクを完了させることができる。
タスクの追加ができる。
-->