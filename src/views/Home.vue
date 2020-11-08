<template>
  <div class="todo-list">
    <h3>新增待办</h3>
    <div class="input-box">
      <label>待办事物</label>
      <input type="text" v-model="state.todo" @keyup.enter="addTodo" />
    </div>

    <h3>待办列表</h3>
    <ul>
      <li
        v-for="todo in todos"
        :key="todo.id"
        @click="changeStatus(todo, true)"
      >
        {{ todo.text }}
      </li>
    </ul>

    <h3>已办事物</h3>
    <ul>
      <li
        v-for="done in dones"
        :key="done.id"
        @click="changeStatus(done, false)"
      >
        {{ done.text }}
      </li>
    </ul>

    <button @click="jumpToPage({ name: 'About' })">跳转About</button>
    <button @click="jumpToPage({ name: 'Page', query: { id: 9 } })">
      跳转Page
    </button>
  </div>
</template>

<script lang="ts">
import { reactive, computed, toRef } from "vue";
import { RouteLocationRaw, useRouter } from "vue-router";

export default {
  name: "Home",
  setup() {
    const state = reactive({
      todo: "",
      todoList: [
        {
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

    const { todo, todoList } = state;

    const todos = computed(() => todoList.filter((item) => !item.done));

    const dones = computed(() => todoList.filter((item) => item.done));

    const changeStatus = (
      item: { id: number; done: boolean; text: string },
      status: boolean
    ) => {
      item.done = status;
    };

    const addTodo = (e: Event) => {
      const id = todoList[todoList.length - 1].id + 1;
      const data = {
        id,
        done: false,
        text: todo,
      };
      todoList.push(data);
      state.todo = "";
    };

    const router = useRouter();
    const jumpToPage = (query: RouteLocationRaw) => {
      router.push(query);
    };

    return {
      state,
      todos,
      dones,
      changeStatus,
      addTodo,
      jumpToPage,
    };
  },
};
</script>
