<template>
  <div>
    <h2>Tasks</h2>

    <Button
      @handle-click="$emit('handleClick')"
      :text="showAdd ? 'close' : 'Add Task'"
      :color="showAdd ? 'red' : 'green'"
    />
  </div>
</template>

<script>
import Button from "./Button.vue";
export default {
  name: "Header",
  props: {
    showAdd: Boolean,
  },
  components: {
    Button,
  },
};
</script>

<style scoped>
div {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin: auto;
}
</style>
