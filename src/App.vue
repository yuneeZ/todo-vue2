<template>
  <div id="app">
    <TodoHeader></TodoHeader>
    <TodoInput></TodoInput>
    <TodoList></TodoList>
    <TodoFooter></TodoFooter>
  </div>
</template>

<script>
import TodoFooter from "./components/TodoFooter.vue";
import TodoHeader from "./components/TodoHeader.vue";
import TodoInput from "./components/TodoInput.vue";
import TodoList from "./components/TodoList.vue";

export default {
  components: {
    TodoHeader: TodoHeader,
    TodoInput: TodoInput,
    TodoList: TodoList,
    TodoFooter: TodoFooter,
  },
};
</script>

<style>
body {
  margin: 0;
  background: #eee;
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #222;
}

body * {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

input,
button {
  border: 0;
}

.shadow {
  box-shadow: 5px 10px 10px rgba(0, 0, 0, 0.03);
  box-shadow: 5px 10px 10px rgba(0, 0, 0, 0.8);
}

.blind {
  position: absolute;
  overflow: hidden;
  clip: rect(0 0 0 0);
  margin: -1px;
  width: 1px;
  height: 1px;
  font-size: 6px;
  line-height: 1;
  white-space: nowrap;
}

#app {
  padding: 0 10px;
}
</style>
