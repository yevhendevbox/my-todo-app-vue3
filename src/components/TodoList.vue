<template>
  <div class="container flex">
    <TodoInput @on-add-task="addTask" />
    <ul class="todo-list">
      <li v-for="todo in todoList" :key="todo.id">
        <TodoItem  :model="todo" @on-done="setDoneTask(todo.id)" @on-remove="removeTask(todo.id)" @uncheck="setDoneTask(todo.id)"/>
      </li>
    </ul>
  </div>
</template>

<script lang="ts">
import TodoInput from "@/components/TodoInput.vue";
import TodoItem from "@/components/TodoItem.vue";
import TodoListType from "@/types/types.ts";
import TaskType from "@/types/types.ts";
import { defineComponent, ref } from "@vue/runtime-core";

export default defineComponent({
  components: {
    TodoInput,
    TodoItem,
  },
  setup() {
    const todoList = ref([
      {
        id: 1,
        title: "Shoping day",
        description: "Go to grocery store to buy some food and staff",
        isDone: false,
      },
      {
        id: 2,
        title: "Learn Vue 3",
        description:
          "Practicing Vue 3 applications, Composition API concepts, Vuex...",
        isDone: false,
      },
      {
        id: 3,
        title: "Everyday gym",
        description: "Go to gym for everyday exercices, health care staff",
        isDone: false,
      },
    ] as Array<TodoListType>);

    const addTask = (task: TaskType): void => {
      const lastId = todoList.value.length - 1;
      todoList.value = [
        ...todoList.value,
        {
          id: todoList.value[lastId].id + 1,
          title: task.title,
          description: task.description,
          isDone: false,
        },
      ];
    };

    const setDoneTask = (id: number): void => {
      todoList.value = todoList.value.map((task) => {
        if (task.id === id) {
          task.isDone = !task.isDone;
        }
        return task;
      });
    };

    const removeTask = (id: number): void => {
      const indexToRemove = todoList.value.findIndex((task) => task.id === id);
      todoList.value.splice(indexToRemove, 1);
    };

    return { todoList, setDoneTask, removeTask, addTask };
  },
});
</script>

<style scoped>
.todo-list {
  width: 100%;
  list-style: none;
}
.flex {
  display: flex;
  font-size: 1.4rem;
  padding-top: 2em;
}
</style>