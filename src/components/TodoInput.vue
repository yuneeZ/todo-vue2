<template>
  <div>
    <div class="inputBox">
      <input
        type="text"
        placeholder="Type what you have to do"
        ref="todoInput"
        v-model="newTodoItem"
        v-on:keypress.enter="addTodo"
      />
      <button type="button" class="btnAdd" v-on:click="addTodo">
        <span class="btnAddIcon fas fa-plus"></span>
        <span class="blind">추가</span>
      </button>
    </div>
    <modal v-if="showModal" v-on:click="handleCloseModal">
      <h3 slot="header">알림</h3>
      <div slot="body">
        <p>할 일을 입력해주세요</p>
        <button
          type="button"
          ref="modalCloseButton"
          v-on:click="handleCloseModal"
          class="btnClose"
        >
          <span class="blind">닫기</span>
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
      const trimmedValue = this.newTodoItem.trim();
      if (trimmedValue) {
        this.$emit("addTodo", trimmedValue);
      } else {
        this.showModal = !this.showModal;
      }
      this.clearInput();
    },
    clearInput() {
      this.newTodoItem = "";
    },
    handleCloseModal() {
      this.showModal = false;
      this.$nextTick(() => {
        this.$refs.todoInput.focus();
      });
    },
  },
  components: {
    modal: Modal,
  },
  mounted() {
    this.$refs.todoInput.focus();
  },
  watch: {
    showModal: function () {
      this.$refs.todoInput.focus();
    },
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
  line-height: 40px;
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
.btnClose {
  position: absolute;
  top: 5px;
  right: 5px;
  width: 40px;
  height: 40px;
  background: none;
}
.btnClose:before,
.btnClose:after {
  position: absolute;
  top: 50%;
  left: 50%;
  width: 2px;
  height: 20px;
  margin-top: -10px;
  background: #000;
  content: "";
}
.btnClose:before {
  transform: rotate(45deg);
}
.btnClose:after {
  transform: rotate(-45deg);
}
</style>
