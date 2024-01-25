<template>
  <transition-group name="list" tag="ul">
    <!-- <li v-for="(todoItem, index) in todoItems" class="todoList"> -->
    <!-- App 컴포넌트의 TodoItems 데이터 개수만큼 반복되도록 목록 아이템 생성 -->
    <li v-for="(todoItem, index) in propsData" :key="todoItem" class="todoList">
      <span class="iconCheck fas fa-check"></span>
      <span>{{ todoItem }}</span>
      <button
        type="button"
        class="btnDelete"
        @click="removeTodo(todoItem, index)"
      >
        <span class="blind">삭제</span>
        <span class="iconDelete far fa-trash-alt"></span>
      </button>
    </li>
  </transition-group>
</template>

<script>
export default {
  props: ["propsData"],
  methods: {
    removeTodo(todoItem, index) {
      this.$emit("removeTodo", todoItem, index);
      // App 컴포넌트에서 관리
      // localStorage.removeItem(todoItem);
      // this.todoItems.splice(index, 1);
    },
  },
  // App 컴포넌트에서 관리
  // data() {
  //   return {
  //     todoItems: [],
  //   };
  // },
  // created() {
  //   if (localStorage.length > 0) {
  //     for (var i = 0; i < localStorage.length; i++) {
  //       this.todoItems.push(localStorage.key(i));
  //     }
  //   }
  // },
};
</script>

<style>
.todoList {
  display: flex;
  height: 40px;
  margin-top: 10px;
  padding-left: 10px;
  border-radius: 5px;
  background: #fff;
  text-align: left;
  align-items: center;
}
.iconCheck {
  margin-right: 10px;
  color: #8763fb;
}
.btnDelete {
  width: 40px;
  height: 40px;
  margin-left: auto;
  background: none;
}
.list-enter-active,
.list-leave-active {
  transition: all 0.3s;
}
.list-enter,
.list-leave-to {
  opacity: 0;
  transform: translateY(-30px);
}
</style>
