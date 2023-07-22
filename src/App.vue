<template>
  <div class="container">
    <h2>To-Do List</h2>
    <TodoSimpleForm @add-todo="addTodo" />
    
    <div v-if="!todos.length">
      저장된 Todo가 없습니다.
    </div>
    <div 
      class="card mt-2" 
      v-for="(todo,index) in todos" 
      :key="todo.id"
    >
      <div class="card-body p-2 d-flex align-items-center">
        <div class="form-check flex-grow-1">
          <input 
            class="form-check-input"
            type="checkbox"
            v-model = "todo.completed"  
          >
          <label 
            :class="{todo : todo.completed}"
            class="form-check-label"
            for=""
          >
            {{ todo.subject}} 
          </label>
        </div>
        <div>
          <button 
            class="btn btn-danger btn-sm"
            @click = "deleteTodo(index,todo.id)"
            >
            삭제
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { ref } from 'vue';
import TodoSimpleForm from './components/TodoSimpleForm.vue';
export default {
  components:{
    TodoSimpleForm
  },
  setup(){
    
    const todos = ref([]);
    
    const addTodo = (todo) =>{
      console.log(todo)
      todos.value.push(todo)
    }
    
    const deleteTodo = (index,id) => {
      todos.value.splice(index,1);
      console.log(id)

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