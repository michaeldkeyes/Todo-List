<template>
  <div class="todo-item">
    <button class="checkbox" @click="deleteFromTodos" />
    <div class="text-rules">
      {{ title }}
    </div>
  </div>
</template>

<script>
export default {
  name: "Todo",
  props: ["title", "id"],
  methods: {
    deleteFromTodos() {
      this.$emit("deleteTodo", this.id);
    },
  },
};
</script>

<style lang="scss" scoped>
input {
  position: absolute;
  opacity: 0;
  cursor: pointer;
  height: 0;
  width: 0;
}

.checkbox {
  background-color: transparent;
  border: 1px solid grey;
  border-radius: 16px;
  color: grey;
  cursor: pointer;
  height: 18px;
  margin: 5px 10px 0 0;
  width: 18px;
}

button:hover {
  background-color: #ccc;
}

.todo-item {
  border-bottom: 1px solid #f0f0f0;
  border-color: hsla(0, 0%, 100%, 0.1);
  cursor: pointer;
  display: flex;
  align-items: center;
  font-size: 1.4rem;
  padding: 16px 0;
}

.text-rules {
  word-break: break-word;
  word-wrap: break-word;
}
</style>
