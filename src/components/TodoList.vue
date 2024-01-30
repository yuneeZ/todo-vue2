<template>
  <transition-group name="list" tag="ul">
    <li
      v-for="(todoItem, index) in propsData"
      v-bind:key="todoItem"
      class="todoList"
    >
      <span class="iconCheck fas fa-check"></span>
      <span>{{ todoItem }}</span>
      <button
        type="button"
        class="btnDelete"
        v-on:click="clearItem(todoItem, index)"
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
    clearItem(todoItem, index) {
      // App으로 이벤트 전달
      // localStorage.removeItem(todoItem);
      // this.todoItems.splice(index, 1);
      this.$emit("clearItem", todoItem, index);
    },
  },
  // App에서 리스트 관리
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
