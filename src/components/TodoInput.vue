<!-- 할일 입력 및 추가 -->
<template>
<div class="inputBox shadow">
  <input type="text" 
  v-model="newTodoItem" 
  placeholder="Type what you have to do"
  v-on:keyup.enter="addTodo"/>
  <span class="addContainer" @click="addTodo" >
    <i class="addBtn fas fa-plus" aria-hidden="true"></i>
  </span>

  <!-- 경고 모달창 -->
  <modal :show="showModal" @close="showModal = false">
    <template #header>
      <h3>WARNING!</h3>
    </template>
    <template #footer @click="showModal =false">
      <span class="msg">할 일을 입력하세요!</span>
    </template>
  </modal>
</div>
</template>

<script>
import Modal from './common/Modal.vue'

export default {
  props: ['propsdata'],
  components: {
    // 모달 컴포넌트 추가
    Modal
  },
  data() {
    return {
      newTodoItem: '',
      showModal: false  // 모달 동작을 위한 플래그 값
    }
  },
  methods: {
    addTodo() {
      const todo = this.newTodoItem;
      if(todo !== "") { // 입력값이 있을때만 저장하도록!
        var value = todo && todo.trim(); // 입력된 텍스트 앞뒤 공백 문자열제거
        this.$emit('addTodo',value);
        this.clearInput();
      } else {
        this.showModal = !this.showModal; // 텍스트 미입력시 모달 동작
      }
    },
    clearInput() { // 입력값 초기화
      this.newTodoItem = '';
    }
  }
}
</script>

<style scoped>
  .msg {
    display: inline-block;
    margin-left: 30px;
    padding-bottom: 30px;
  }
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