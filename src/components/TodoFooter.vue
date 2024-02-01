<template>
  <div class="btnBox">
    <button type="button" class="btnDeleteSelected" v-on:click="clearSelected">
      선택된 항목 삭제
    </button>
    <button type="button" class="btnDeleteAll" v-on:click="clearAll">
      전체 삭제
    </button>
  </div>
</template>

<script>
export default {
  methods: {
    clearAll() {
      this.$emit("clearAll");
    },
    clearSelected() {
      console.log("");
    },
  },
};
</script>

<style>
.btnBox {
  margin-top: 30px;
}
.btnBox button {
  height: 35px;
  padding: 0 10px;
  border-radius: 5px;
  font-weight: bold;
  color: #fff;
  cursor: pointer;
}
.btnDeleteSelected {
  background: #d99b9b;
}
.btnDeleteAll {
  background: #bd4141;
}
</style>
