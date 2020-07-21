<template>
  <div id="app">
    <TodoList />
  </div>
</template>

<script>
import TodoList from "./components/TodoList";

export default {
  name: "App",
  components: {
    TodoList,
  },
};
</script>

<style>
* {
  box-sizing: border-box;
  font-size: 1em;
  font-family: inherit;
  margin: 0;
  padding: 0;
}

html {
  font-size: 62.5%;
}

body {
  background-color: #1f1f1f;
  color: hsla(0, 0%, 100%, 0.87);
}

ol,
ul {
  list-style: none;
}

img {
  max-width: 100%;
  height: auto;
}

#app {
  font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Oxygen,
    Ubuntu, Cantarell, "Open Sans", "Helvetica Neue", sans-serif;
}
</style>
