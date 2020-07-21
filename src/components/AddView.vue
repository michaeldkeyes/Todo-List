<template>
  <div class="m-t-5">
    <form>
      <input
        type="text"
        placeholder="e.g. Buy gift tomorrow"
        ref="thingy"
        v-model="newTodo"
      />
    </form>
    <div class="p-t-10">
      <button
        type="submit"
        class="red-button"
        :class="{ highlight: isTyping }"
        @click="addToTodoList"
      >
        Add Task
      </button>
      <button type="button" class="cancel" @click="$emit('cancelView')">
        Cancel
      </button>
    </div>
  </div>
</template>

<script>
export default {
  name: "AddView",
  mounted() {
    this.focusInput();
  },
  data() {
    return {
      newTodo: "",
      isTyping: false,
    };
  },
  methods: {
    focusInput() {
      this.$nextTick(() => {
        this.$refs.thingy.focus();
      });
    },
    addToTodoList() {
      this.$emit("addTodo", this.newTodo);
      this.newTodo = "";
      this.$refs.thingy.focus();
    },
  },
  watch: {
    newTodo: function() {
      if (this.newTodo.length > 0) {
        this.isTyping = true;
      } else {
        this.isTyping = false;
      }
    },
  },
};
</script>

<style lang="scss" scoped>
form {
  background-color: #171717;
  border: 1px solid #444;
  border-radius: 5px;
  cursor: text;
  padding: 10px 10px 0;
  word-break: break-word;
  word-wrap: break-word;
}

input {
  background-color: #171717;
  border: none;
  color: rgba(255, 255, 255, 0.4);
  font-size: 1.4rem;
  line-height: 2.1rem;
  padding-bottom: 10px;
  width: 100%;
  word-break: break-word;
  word-wrap: break-word;

  &:focus {
    color: rgba(255, 255, 255, 0.9);
  }
}

button {
  background-color: transparent;
  border: none;
  color: rgba(255, 255, 255, 0.4);
  cursor: pointer;
  font-size: 1.3rem;
}

.p-t-10 {
  padding: 10px 0 0;
}

.red-button {
  background-color: #de4c4a;
  border: 1px solid transparent;
  border-radius: 3px;
  color: #fff;
  font-weight: 700;
  line-height: 17px;
  margin-right: 5px;
  padding: 6px 12px 7px;
  opacity: 0.3;
}

.highlight {
  opacity: 1;
}

.cancel {
  padding: 2px 5px;
}

.m-t-5 {
  margin-top: 5px;
}
</style>
