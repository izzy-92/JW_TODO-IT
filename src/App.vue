<template>
  <div id="app">
    <TodoHeader/>
    <TodoInput v-on:addTodo="addTodo"/>
    <TodoList v-bind:propsdata="todoItems" @removeTodo="removeTodo"/>
    <TodoFooter v-on:removeAll="clearAll"/>
  </div>

</template>

<script>
import TodoHeader from './components/TodoHeader.vue'
import TodoInput from './components/TodoInput.vue'
import TodoList from './components/TodoList.vue'
import TodoFooter from './components/TodoFooter.vue'

export default {
  data() {
    return {
      todoItems: []
    }
  },
  created() { // 뷰 인스턴스 생성되자마자 뷰 데이터에 접근하는 라이프사이클
    const putIn = localStorage.length;
    if(putIn > 0) {
      for(var i = 0; i < putIn; i++) {
        this.todoItems.push(localStorage.key(i));
      }
    }
  },
  methods: {
    // 로컬 스토리지에 데이터를 추가하는 로직
    addTodo(todoItem) {
      localStorage.setItem(todoItem, todoItem);
      this.todoItems.push(todoItem);
    },
    clearAll() {
      localStorage.clear();
      this.todoItems = [];
    },
    removeTodo(todoItem, index) {
      localStorage.removeItem(todoItem);
      this.todoItems.splice(index , 1);
    }
  },
  components: {
    TodoHeader,
    TodoInput,
    TodoList,
    TodoFooter
  }
}
</script>

<style>
body {
  text-align: center;
  background-color: #f6f6f8;

}
input {
  width: 200px;
  border-style: groove;
}
button {
  border-style: groove;
}
.shadow {
  box-shadow: 5px 10px 10px rgba(0, 0, 0, .3)
}
</style>