<!-- 할일 목록 표시 및 특정 할일 삭제 -->
<template>
  <section>
    <transition-group name="list" tag="ul">
      <li 
      v-for="(todoItem, index) in propsdata" 
      :key="todoItem" class="shadow">
      <!-- 할일 목록 체크 -->
      <i class="checkBtn fas fa-check" aria-hidden="true"></i>
      {{ todoItem }}
      <!-- 할일 목록 & 삭제 버튼 마크업 작업 -->
      <span class="removeBtn" type="button"
        @click="removeTodo(todoItem, index)">
          <i class="far fa-trash-alt" aria-hidden="true"></i>
        </span>
      </li>
    </transition-group>
  </section>
</template>

<script>
// 로컬 스토리지 데이터를 뷰 데이터에 저장하는 코드
export default { 
  props: ['propsdata'],
  methods: {
    removeTodo(todoItem, index) {
      this.$emit('removeTodo', todoItem, index)
    }

  }
}
</script>

<style scoped>
  .list-enter-active,
  .list-leave-active {
     transition: all 1s;
  }
  .list-enter,
  .list-leave-to {
    opacity: 0;
    transform: translateY(30px);
  }
  ul {
    list-style-type: none;
    padding-left: 0px;
    margin-top: 1px;
    text-align: left;
  }

  li {
    display: flex;
    height: 50px;
    min-height: 50px;
    line-height: 50px;
    margin: 0.5rem 0;
    padding: 0 0.9rem;
    background: rgb(248, 235, 248);
    border-radius: 5px;
  }

  .checkBtn {
    line-height: 45px;
    margin-right: 7px;
    color: #62acde;
  }
  
  .removeBtn {
    margin-left: auto;
    color: #de4343;
  }
</style>