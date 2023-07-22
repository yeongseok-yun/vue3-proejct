<template>
  <div class="container">
    <h2>To-Do List</h2>
    <form 
    @submit.prevent="onSubmit"
      >
      <div class="d-flex">
        <div class="flex-grow-1 mr-2">
          <input 
            class="form-control"
            type="text" 
            v-model = "todo"
            placeholder = "Type new to-do"
          >
        </div>
        <div>
          <button 
            class = "btn btn-primary"
            type="submit"
          >
          추가
          </button>
        </div>
      </div>
      <div v-show = "hasError" style="color:red;">This field cannot be empty.</div>
    </form>
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
export default {
  setup(){
    const todo = ref('');
    const todos = ref([]);
    const hasError = ref(false);
    const todoStyle = {
      textDecoration : 'line-through',
      color : 'gray'
    };
    const onSubmit = () => {
      if(todo.value === ''){
        hasError.value = true
      }else{
        todos.value.push({
          id: Date.now(),
          subject : todo.value,
          completed : false,
        })
        hasError.value = false
        todo.value = ''
      }
      
    }
    const deleteTodo = (index,id) => {
      todos.value.splice(index,1);
      console.log(id)

    }

    return {
      todo,
      todos,
      onSubmit,
      hasError,
      todoStyle,
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