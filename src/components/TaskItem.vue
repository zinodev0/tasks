<template>
  <div
    :style="{ 'background-color': task.completed ? '#c2fcb2' : '#faebd7' }"
    class="task__item"
  >
    <div class="task__item__text">
      <h3 @click="$emit('completed', task.id)">{{ task.title }}</h3>
      <p>{{ task.description }}</p>
    </div>

    <button @click="$emit('delete', task.id)">X</button>
  </div>
</template>

<script>
export default {
  name: "TaskItem",
  props: {
    task: Object,
  },
};
</script>

<style scoped>
.task__item {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-top: 10px;
}

h3,
p {
  margin: 4px 10px;
}

.task__item__text {
  display: flex;
  flex-direction: column;
  align-items: flex-start;
}

button {
  height: fit-content;
  margin-right: 20px;
  color: white;
  background-color: red;
  border: none;
  padding: 5px 10px;
  cursor: pointer;
}

button:hover {
  transform: scale(0.9, 0.8);
  transition: 0.24s ease-in-out;
}
</style>
