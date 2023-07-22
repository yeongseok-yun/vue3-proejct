<template>
  <div class="container">
    <h2>To-Do List</h2>
    <TodoSimpleForm @add-todo="addTodo" />
    
    <div v-if="!todos.length">
      저장된 Todo가 없습니다.
    </div>
    <TodoList :todos="todos" @toggle-todo = "deleteTodo"/>
  </div>
</template>

<script>
import { ref } from 'vue';
import TodoSimpleForm from './components/TodoSimpleForm.vue';
import TodoList from './components/TodoList.vue';
export default {
  components:{
    TodoSimpleForm,
    TodoList,
  },
  setup(){
    
    const todos = ref([]);
    
    const addTodo = (todo) =>{
      console.log(todo)
      todos.value.push(todo)
    }
    
    const deleteTodo = (todoObj) => {
      todos.value.splice(todoObj.index,1);
      console.log(todoObj.id)

    }

    return {
      todos,
      addTodo,
      deleteTodo
    }
  }
}
</script>

<style>
.todo{
  color:gray;
  text-decoration: line-through;
}
</style>