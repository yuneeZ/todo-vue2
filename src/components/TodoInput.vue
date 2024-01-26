<template>
  <div>
    <div class="inputBox">
      <input
        type="text"
        placeholder="Type what you have to do"
        v-model="newTodoItem"
        v-on:keydown.enter="addTodo"
      />
      <button type="button" class="btnAdd" v-on:click="addTodo">
        <span class="btnAddIcon fas fa-plus"></span>
        <span class="blind">추가</span>
      </button>
    </div>
    <modal v-if="showModal" v-on:close="showModal = false">
      <h3 slot="header">알림</h3>
      <div slot="body">
        <p>할 일을 입력해주세요</p>
        <button type="button" v-on:click="showModal = false">
          <span class="blind">닫기</span>
          <span class="fas fa-times"></span>
        </button>
      </div>
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
        // 텍스트 앞 뒤 공백 문자열 제거
        var value = this.newTodoItem && this.newTodoItem.trim();
        // App으로 이벤트 전달
        // localStorage.setItem(value, value);
        this.$emit("addTodo", value);
      } else {
        this.showModal = !this.showModal;
      }
      this.clearInput();
    },
    clearInput() {
      this.newTodoItem = "";
    },
  },
  components: {
    modal: Modal,
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
