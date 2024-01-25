<template>
  <div class="inputBox">
    <input
      type="text"
      v-model="newTodoItem"
      placeholder="Type what you have to do"
      v-on:keyup.enter="addTodo"
    />
    <button type="button" v-on:click="addTodo" class="btnAdd">
      <span class="btnAddIcon fas fa-plus"></span>
      <span class="blind">추가</span>
    </button>
    <modal v-if="showModal" @close="showModal = false">
      <h3 slot="header">알림</h3>
      <p slot="footer" @click="showModal = false">
        할 일을 입력하세요.
        <button type="button" class="btnClose">
          <span class="fas fa-times"></span>
        </button>
      </p>
    </modal>
  </div>
</template>

<script>
import Modal from "./common/Modal";

export default {
  data() {
    return {
      newTodoItem: "",
      showModal: false,
    };
  },
  methods: {
    addTodo() {
      if (this.newTodoItem.trim() !== "") {
        // 텍스트의 앞 뒤 공백 문자열 제거
        var value = this.newTodoItem && this.newTodoItem.trim();
        // TodoInput에선 이벤트만 전달
        // localStorage.setItem(value, value);
        this.$emit("addTodo", value);
        this.clearInput();
      } else {
        this.showModal = !this.showModal;
      }
    },
    clearInput() {
      this.newTodoItem = "";
    },
  },
  components: {
    Modal: Modal,
  },
};
</script>

<style>
.inputBox {
  display: flex;
}
.inputBox input {
  height: 40px;
  padding: 0 10px;
  background: #fff;
  border-radius: 5px 0 0 5px;
  flex: 1;
}
.btnAdd {
  width: 40px;
  height: 40px;
  border-radius: 0 5px 5px 0;
  background: #8763fb;
}
.btnAddIcon {
  color: #fff;
}
</style>
