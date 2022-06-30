<template>
  <form @submit="addTask">
    <div>
      <input type="text" placeholder="Task Title" v-model="title" />
      <textarea
        maxlength="100"
        rows="2"
        cols="25"
        placeholder="Task Description"
        v-model="description"
      />

      <label for="completed">
        Completed:
        <input
          type="checkbox"
          name="completed"
          id="completed"
          v-model="completed"
        />
      </label>
      <button :disabled="!title || !description" @click="addTask">Save</button>
    </div>
  </form>
</template>

<script>
export default {
  name: "AddTask",
  data() {
    return {
      title: "",
      description: "",
      completed: false,
    };
  },
  methods: {
    addTask(e) {
      e.preventDefault();
      console.log("add");

      const newTask = {
        title: this.title,
        description: this.description,
        completed: this.completed,
      };

      this.$emit("add-task", newTask);

      this.title = "";
      this.description = "";
      this.completed = false;
    },
  },
};
</script>

<style scoped>
div {
  display: flex;
  flex-direction: column;
  align-items: flex-start;
}

input,
textarea {
  margin-top: 20px;
  font-size: 18px;
  padding: 10px;
}

button {
  width: fit-content;
  padding: 5px 15px;
  margin: 20px 0px;
}
label {
  white-space: normal;
  display: inline-block;
  font-size: 20px;
}
input[type="checkbox"] {
  width: 18px;
  height: 18px;
}
</style>
