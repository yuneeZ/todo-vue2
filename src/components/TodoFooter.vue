<template>
  <div class="btnBox">
    <button type="button" class="btnDeleteAll" v-on:click="clearAll">
      Clear All
    </button>
  </div>
</template>

<script>
export default {
  methods: {
    clearAll() {
      // App으로 이벤트 전달
      // localStorage.clear();
      this.$emit("clearAll");
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
