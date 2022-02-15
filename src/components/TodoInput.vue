<template>
  <div class="todo-form">
     <span class="p-float-label">
            <InputText id="taskTitle" type="text" v-model="newTask.title"/>
            <label for="taskTitle">Task title</label>
      </span>
       <span class="p-float-label">
            <InputText id="description" type="text" v-model="newTask.description"/>
            <label for="description">Task description</label>
        </span>
        <Button label="Add task" icon="pi pi-check" class="p-button-lg p-button-primary" @click="onAddTask" :disabled="!valid"/>
  </div>
</template>

<script lang="ts">
import { defineComponent, computed, reactive } from "@vue/runtime-core";
import InputText from "primevue/inputtext";
import Button from "primevue/button";
import TaskType from "@/types/types.ts";

export default defineComponent({
  emits: ["onAddTask"],

  components: {
    InputText,
    Button,
  },
  setup(props, { emit }) {
    const newTask = reactive({ title: "", description: "" } as TaskType);

    const onAddTask = () => {
      emit("onAddTask", newTask);
      newTask.title = "";
      newTask.description = "";
    };

    const valid = computed(() => {
      return newTask.title && newTask.description;
    });

    return {
      newTask,
      onAddTask,
      valid,
    };
  },
});
</script>

<style scoped>
.todo-form {
  min-width: 35%;
  padding: 3em 1em;
}
.todo-form * {
  width: 100%;
  margin-bottom: 1em;
}
.todo-form input {
  padding: 1em;
  font-size: 1.6rem;
}
</style>