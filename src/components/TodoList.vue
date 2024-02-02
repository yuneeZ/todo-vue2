<template>
  <transition-group name="list" tag="ul">
    <li
      v-for="(todoItem, index) in propsData"
      v-bind:key="todoItem.key"
      class="todoList"
    >
      <div class="checkBox">
        <input
          type="checkbox"
          class="checkBoxInput"
          v-bind:id="todoItem.key"
          v-bind:value="todoItem.key"
          v-model="checkedTodo"
        />
        <label class="checkBoxLabel" v-bind:for="todoItem.key">{{
          todoItem.value
        }}</label>
      </div>
      <button type="button" class="btnDelete" v-on:click="clearItem(index)">
        <span class="blind">삭제</span>
        <span class="iconDelete far fa-trash-alt"></span>
      </button>
    </li>
  </transition-group>
</template>

<script>
export default {
  props: ["propsData"],
  data() {
    return {
      checkedTodo: [],
    };
  },
  methods: {
    clearItem(todoItem, index) {
      this.$emit("clearItem", todoItem, index);
    },
    selectedTodo() {
      this.$emit("selectedTodo", this.checkedTodo);
    },
  },
  watch: {
    checkedTodo: {
      handler() {
        this.selectedTodo();
      },
      deep: true,
    },
  },
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
.checkBoxInput:checked + .checkBoxLabel:before {
  background: #8763fb;
  border-color: #8763fb;
}
.checkBoxInput:checked + .checkBoxLabel:after {
  border-color: #fff;
}
</style>
