<template>
  <div class="btnBox">
    <button type="button" class="btnDeleteAll" @click="clearAllTodo">
      Clear All
    </button>
  </div>
</template>

<script>
export default {
  methods: {
    clearAllTodo() {
      // 이벤트 전달
      // localStorage.clear();
      this.$emit("clearAllTodo");
      console.log("a");
    },
  },
};
</script>

<style>
.btnBox {
  margin-top: 30px;
}
.btnDeleteAll {
  height: 35px;
  padding: 0 10px;
  border-radius: 5px;
  background: #bd4141;
  font-weight: bold;
  color: #fff;
}
</style>
