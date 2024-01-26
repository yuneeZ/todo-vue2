<template>
  <div id="app">
    <TodoHeader></TodoHeader>
    <TodoInput v-on:addTodo="addTodo"></TodoInput>
    <TodoList
      v-bind:propsData="todoItems"
      v-on:clearItem="clearItem"
    ></TodoList>
    <TodoFooter v-on:clearAll="clearAll"></TodoFooter>
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
  data() {
    return {
      todoItems: [],
    };
  },
  methods: {
    // todo 아이템 추가 - TodoInput 컴포넌트에서 보낸 이벤트
    addTodo(todoItem) {
      // TodoInput 컴포넌트에서 올려 보낸 값을 로컬 스토리지에 추가
      localStorage.setItem(todoItem, todoItem);
      this.todoItems.push(todoItem);
    },
    // todo 아이템 삭제 - TodoList 컴포넌트에서 보낸 이벤트
    clearItem(todoItem, index) {
      localStorage.removeItem(todoItem);
      this.todoItems.splice(index, 1);
    },
    // todo 아이템 전체 삭제 - TodoFooter 컴포넌트에서 보낸 이벤트
    clearAll() {
      localStorage.clear();
      this.todoItems = [];
    },
  },
  created() {
    if (localStorage.length > 0) {
      for (var i = 0; i < localStorage.length; i++) {
        this.todoItems.push(localStorage.key(i));
      }
    }
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
  font-size: 14px;
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
  font-size: 14px;
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
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
