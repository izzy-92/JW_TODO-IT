<!-- 할일 모두 삭제 -->
<template>
  <div class="clearAllContainer">
    <span class="clearAllBtn" @click="clearTodo">Clear All</span>
  </div>
</template>

<script>
export default {
  methods: {
    clearTodo() {
      this.$emit('removeAll');
    }
  }
}
</script>

<style scoped>
  .clearAllContainer {
    width: 8.5rem;
    height: 50px;
    line-height: 50px;
    background-color: rgb(252, 221, 164);
    border-radius: 5px;
    margin: 0 auto;
  }

  .clearAllBtn {
    display: block;
    color: #e92727;
    font-weight: 800;
  }

</style>