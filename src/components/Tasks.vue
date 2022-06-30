<template>
  <div :key="task.id" v-for="task in tasks">
    <TaskItem
      @completed="$emit('toggle-complete', task.id)"
      @delete="$emit('delete-task', task.id)"
      :task="task"
    />
  </div>
</template>

<script>
import TaskItem from "./TaskItem.vue";

export default {
  name: "Tasks",
  components: { TaskItem },
  props: {
    tasks: Array,
  },

  emits: ["delete-task", "toggle-complete"],
};
</script>

<style></style>
