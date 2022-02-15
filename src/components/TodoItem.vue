<template>
  <div class="todo-item">
        <Fieldset :legend="model.title">
            <div class="task-wrapper">
              <p :class="{done: model.isDone}">{{ model.description }}</p>
              <div class="btns">
                <Button icon="pi pi-check" class="p-button-primary" @click="onDone" v-if="!model.isDone"/>
                <Button icon="pi pi-undo" class="p-button-primary" @click="unCheck" v-else/>
                <Button icon="pi pi-times" class="p-button-danger" @click="onRemove" :disabled="!model.isDone"/>
              </div>
            </div>

        </Fieldset>
  </div>
</template>

<script lang="ts">
import { defineComponent } from "@vue/runtime-core";
import Fieldset from "primevue/fieldset";
import Button from "primevue/button";

export default defineComponent({
  components: {
    Fieldset,
    Button,
  },
  emits: ["on-done", "on-remove", "uncheck"],
  props: {
    model: {
      required: true,
      default: {
        id: 0,
        title: "Create todo app",
        description: "todo app using Vue 3 & Composition API",
        isDone: false,
      },
    },
  },
  setup(props, { emit }) {
    const onDone = (): void => {
      emit("on-done");
    };

    const onRemove = (): void => {
      emit("on-remove");
    };

    const unCheck = (): void => {
      emit("uncheck");
    };

    return { onDone, onRemove, unCheck };
  },
});
</script>

<style scoped>
.todo-item {
  min-width: 55%;
  margin-bottom: 2em;
  font-size: 1.4em;
}
::v-deep(.p-fieldset-content) {
  font-size: 1.4em;
  line-height: 1.7;
}
::v-deep(.p-fieldset-legend-text) {
  font-size: 1.4em;
}
.task-wrapper {
  display: flex;
  justify-content: space-between;
  align-items: center;
  gap: 2em;
}
.btns {
  display: flex;
  gap: 1em;
  flex-direction: column;
}
.done {
  text-decoration-line: line-through;
  opacity: 0.8;
}
</style>