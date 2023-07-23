<template>
  <div class="container">
    <h2>To-Do-List</h2>
    <input 
      class="form-control"
      type="text" 
      v-model = "searchText"
      placeholder = "Search"
    >
    <hr>
    <TodoSimpleForm @add-todo="addTodo" />
    <div style="color:red;">{{ error }}</div>
    <div v-if="!filtedTodos.length">
      등록 된 Todo가 없습니다.
    </div>
    <TodoList :todos="filtedTodos" 
      @toggle-todo = "toggleTodo" 
      @delete-todo = "deleteTodo"
    />
  </div>
</template>

<script>
import { ref, computed } from 'vue';
import TodoSimpleForm from './components/TodoSimpleForm.vue';
import TodoList from './components/TodoList.vue';
import axios from 'axios';

export default {
  components:{
    TodoSimpleForm,
    TodoList,
  },
  setup(){
    
    const todos = ref([]);
    const error = ref('');
    const addTodo = (todo) =>{
      console.log(todo)
      //db 저장
      error.value = '';
      axios.post('http://localhost:3000/todos',{
        subject : todo.subject,
        completed : todo.completed,
      }).then(res =>{
        console.log(res);
        todos.value.push(res.data);
      }).catch(err => {
        console.log(err);
        error.value = '예기치 못한 에러가 발생했습니다.'
      });
      
    }
    
    const toggleTodo = (index) =>{
      todos.value[index].completed = !todos.value[index].completed;
    }
    const deleteTodo = (index) => {
      todos.value.splice(index,1);
    }
    const searchText = ref('');
    const filtedTodos = computed(() => {
      if(searchText.value){
        return todos.value.filter(todo => {
          return todo.subject.includes(searchText.value);
        });
      }
      return todos.value;
    })
    return {
      todos,
      addTodo,
      toggleTodo,
      deleteTodo,
      searchText,
      filtedTodos,
      error,
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