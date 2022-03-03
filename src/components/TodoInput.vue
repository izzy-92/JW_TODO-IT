<!-- 할일 입력 및 추가 -->
<template>
<div class="inputBox shadow">
  <input type="text" 
  v-model="newTodoItem" 
  placeholder="Type what you have to do"
  v-on:keyup.enter="addTodo"/>
  <span class="addContainer" @click="addTodo">
    <i class="addBtn fas fa-plus" aria-hidden="true"></i>
  </span>
</div>
</template>

<script>


export default {
  data() {
    return {
      newTodoItem: ''
    }
  },
  methods: {
    addTodo() {
      const todo = this.newTodoItem;
      if(todo !== "") { // 입력값이 있을때만 저장하도록!
        var value = todo && todo.trim(); // 입력된 텍스트 앞뒤 공백 문자열제거
        this.$emit('addTodo',value);
        //localStorage.setItem(value, value); 로컬 스토리지에 데이터를 저장하는 기존코드는 주석처리.
        this.clearInput();
      }
    },
    clearInput() { // 입력값 초기화
      this.newTodoItem = '';
    }
  }
}
</script>

<style scoped>
  input:focus {
    outline: none;
  }
  .inputBox {
    background: white;
    height: 50px;
    line-height: 50px;
    border-radius: 5px;
  }
  .inputBox input {
    font-size: 0.9rem;
  }
  .addContainer {
    display: block;
    width: 3rem;
    float: right;
    background: linear-gradient(to right, #6478fb, #8763fb);
    border-radius: 0 5px 5px 0;
  }
  .addBtn {
    color: white;
    vertical-align: center;
  }
</style>