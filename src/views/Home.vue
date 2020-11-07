<template>
<div class="todo-list">
    <h3>新增待办</h3>
    <div class="input-box">
        <label>待办事物</label>
        <input type="text" v-model="state.todo" @keyup.enter="addTodo" />
    </div>

    <h3>待办列表</h3>
    <ul>
        <li v-for="todo in todos" :key="todo.id">{{ todo.text }}</li>
    </ul>

    <h3>已办事物</h3>
    <ul>
        <li v-for="done in dones" :key="done.id">{{ done.text }}</li>
    </ul>
</div>
</template>

<script lang="ts">
import {
    reactive,
    computed
} from "vue";
import {
    useRouter
} from "vue-router";

export default {
    name: "Home",
    setup(props, cxt) {
        const state = reactive({
            todo: "",
            todoList: [{
                    id: 1,
                    done: false,
                    text: "吃饭",
                },
                {
                    id: 2,
                    done: false,
                    text: "睡觉",
                },
                {
                    id: 3,
                    done: false,
                    text: "打豆豆",
                },
            ],
        });

        const todos = computed(() => state.todoList.filter((item) => !item.done));

        const dones = computed(() => state.todoList.filter((item) => item.done));

        return {
            state,
            todos,
            dones,
        };
    },
};
</script>
