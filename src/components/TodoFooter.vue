<template>
  <div class="btnBox">
    <button
      type="button"
      class="btnDeleteSelected"
      v-on:click="completeSelected"
    >
      작업 완료
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
    completeSelected() {
      this.$emit("completeSelected");
    },
  },
};
</script>

<style>
.btnBox {
  display: flex;
  margin-top: 30px;
  justify-content: center;
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
  margin: 0 -73px 0 auto;
  background: #d99b9b;
}
.btnDeleteAll {
  margin-left: auto;
  background: #bd4141;
}
</style>
