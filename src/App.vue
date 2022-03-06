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
  created() {
    const list = localStorage.getItem('todoItems');
    if(list) {
      this.todoItems = JSON.parse(list);
    }
  },
  methods: {
    // 로컬 스토리지에 데이터를 추가하는 로직
    addTodo(todoItem) {
      this.todoItems.push(todoItem);
      localStorage.setItem('todoItems', JSON.stringify(this.todoItems));
    },
    clearAll() {
      localStorage.removeItem('todoItems');
      this.todoItems = [];
    },
    removeTodo(todoItem, index) {
      this.todoItems.splice(index , 1);
      localStorage.setItem('todoItems', JSON.stringify(this.todoItems));
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