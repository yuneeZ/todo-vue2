<template>
  <transition-group name="list" tag="ul">
    <li
      v-for="(todoItem, index) in propsData"
      v-bind:key="todoItem.key"
      class="todoList"
    >
      <div class="todoInputElements">
        <div class="checkBox">
          <input
            type="checkbox"
            class="checkBoxInput"
            v-bind:id="todoItem.key"
            v-bind:value="todoItem.key"
            v-model="todoItem.complete"
            v-on:change="checkedTodo"
          />
          <label class="checkBoxLabel" v-bind:for="todoItem.key">
            <span v-if="!isEdit || editingIndex !== index">{{
              todoItem.value
            }}</span>
          </label>
        </div>
        <div
          v-show="isEdit && editingIndex === index"
          class="inputBox inputBox--edit"
        >
          <input
            type="text"
            v-model="editedValue"
            v-on:keyup.enter="submitTodo"
            v-bind:id="'editInput_' + index"
            v-bind:ref="'editInput_' + index"
          />
        </div>
      </div>
      <div class="btnIconBox">
        <button
          type="button"
          class="btnEdit"
          v-on:click="editTodo(todoItem, index)"
          v-bind:disabled="todoItem.complete"
        >
          <span class="blind">수정</span>
          <span class="iconEdit far fa-edit"></span>
        </button>
        <button type="button" class="btnDelete" v-on:click="clearItem(index)">
          <span class="blind">삭제</span>
          <span class="iconDelete far fa-trash-alt"></span>
        </button>
      </div>
    </li>
  </transition-group>
</template>

<script>
export default {
  props: ["propsData"],
  data() {
    return {
      isEdit: false,
      editingIndex: null,
      editedValue: "",
    };
  },
  methods: {
    clearItem(todoItem, index) {
      this.$emit("clearItem", todoItem, index);
    },
    editTodo(todoItem, index) {
      this.isEdit = true;
      this.editingIndex = index;
      this.editedValue = todoItem.value;
    },
    submitTodo() {
      this.isEdit = false;

      if (this.editingIndex !== null) {
        const editedItem = this.propsData[this.editingIndex];
        editedItem.value = this.editedValue;
        this.$emit("editTodo", editedItem);
      }
    },
    checkedTodo() {
      this.$emit("selectedTodo");
    },
  },
};
</script>

<style>
.todoList {
  position: relative;
  display: flex;
  height: 40px;
  margin-top: 10px;
  padding-left: 10px;
  border-radius: 5px;
  background: #fff;
  text-align: left;
  align-items: center;
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
.iconCheck {
  margin-right: 10px;
  color: #8763fb;
}
.btnIconBox {
  margin-left: auto;
  padding: 0 10px;
}
.btnIconBox button {
  width: 30px;
  height: 40px;
  background: none;
}
.btnIconBox .far {
  color: #444;
}
.btnIconBox .btnEdit[disabled] .far {
  color: #999;
}
.todoInputElements {
  position: relative;
  flex: 1;
}
.checkBox {
  position: relative;
  flex: 1;
}
.checkBoxInput {
  position: absolute;
  top: 50%;
  left: 0;
  width: 20px;
  height: 20px;
  opacity: 0;
  transform: translateY(-50%);
}
.checkBoxLabel {
  display: block;
  height: 40px;
  padding-left: 28px;
  line-height: 40px;
  user-select: none;
}
.checkBoxLabel:before,
.checkBoxLabel:after {
  position: absolute;
  box-sizing: border-box;
  content: "";
}
.checkBoxLabel:before {
  top: 50%;
  left: 0;
  width: 20px;
  height: 20px;
  border: 1px solid #999;
  border-radius: 4px;
  transform: translateY(-50%);
}
.checkBoxLabel:after {
  top: 9px;
  left: 5px;
  width: 10px;
  height: 20px;
  border: solid #999;
  border-width: 0 3px 3px 0;
  transform: rotate(45deg) scale(0.5);
}
.checkBoxInput:checked + .checkBoxLabel {
  color: #aaa;
  font-style: italic;
  text-decoration: line-through;
}
.checkBoxInput:checked + .checkBoxLabel:before {
  background: #8763fb;
  border-color: #8763fb;
}
.checkBoxInput:checked + .checkBoxLabel:after {
  border-color: #fff;
}
.inputBox--edit {
  display: block;
  position: absolute;
  top: 0;
  right: 0;
  left: 0;
  background: rgba(255, 0, 0, 0.1);
}
.inputBox--edit input {
  width: 100%;
  padding-left: 28px;
  background: none;
}
</style>
