<template>
  <button @click="handleClick" :style="{ 'background-color': color }">
    {{ text }}
  </button>
</template>

<script>
export default {
  name: "Button",
  props: {
    text: String,
    color: String,
  },
  methods: {
    handleClick() {
      this.$emit("handle-click");
    },
  },
};
</script>

<style scoped>
button {
  padding: 10px 25px;
  height: fit-content;
  cursor: pointer;
  border: none;
  font-size: 16px;
  color: white;
}

button:hover {
  transform: scale(0.9, 0.8);
  transition: 0.24s ease-in-out;
}
</style>
