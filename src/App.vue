<template>
  <div id="app">
    <TodoHeader></TodoHeader>
    <TodoInput v-on:addTodo="addTodo"></TodoInput>
    <TodoList
      v-bind:propsData="todoItems"
      v-on:clearItem="clearItem"
      v-on:selectedTodo="selectedTodo"
      v-on:editTodo="editTodo"
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
      selectedTodoItems: [],
      completedItems: [],
    };
  },
  methods: {
    // todo 아이템 추가 - TodoInput 컴포넌트에서 보낸 이벤트
    addTodo(todoItem) {
      const date = new Date();
      const year = date.getFullYear();
      const month = (date.getMonth() + 1).toString().padStart(2, "0");
      const day = date.getDate().toString().padStart(2, "0");
      const hours = date.getHours().toString().padStart(2, "0");
      const minutes = date.getMinutes().toString().padStart(2, "0");
      const seconds = date.getSeconds().toString().padStart(2, "0");
      const now = year + month + day + hours + minutes + seconds;

      this.todoItems.push({
        key: [this.todoItems.length, now].join("_"),
        value: todoItem,
      });

      // TodoInput 컴포넌트에서 올려 보낸 값을 로컬 스토리지에 배열로 추가
      localStorage.setItem("todoList", JSON.stringify(this.todoItems));
    },
    // todo 아이템 삭제 - TodoList 컴포넌트에서 보낸 이벤트
    clearItem(index) {
      this.todoItems.splice(index, 1);
      localStorage.setItem("todoList", JSON.stringify(this.todoItems));
    },
    // todo 아이템 전체 삭제 - TodoFooter 컴포넌트에서 보낸 이벤트
    clearAll() {
      // localStorage.removeItem("todoList");
      localStorage.clear();
      this.todoItems = [];
    },
    // 선택된 todo 아이템
    selectedTodo(checkedTodo) {
      this.selectedTodoItems = checkedTodo;
      console.log(this.selectedTodoItems);
    },
    // todo 아이템 수정
    editTodo(editedItem) {
      console.log(editedItem.value);
      const index = this.todoItems.findIndex(
        (item) => item.key === editedItem.key
      );

      if (index !== -1) {
        this.todoItems[index] = editedItem;
        localStorage.setItem("todoList", JSON.stringify(this.todoItems));
      }
    },
  },
  created() {
    const getTodoList = localStorage.getItem("todoList");
    const getTodoItem = JSON.parse(getTodoList);

    if (getTodoItem.length > 0) {
      this.todoItems = getTodoItem;
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
