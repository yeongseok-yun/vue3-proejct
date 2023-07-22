<template>
  <div class="container">
    <h2>To-Do List</h2>
    <form 
    @submit="onSubmit"
      class="d-flex"
      >
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

    </form>
    {{todos }}
  </div>
</template>

<script>
import { ref } from 'vue';
export default {
  setup(){
    const todo = ref('');
    const todos = ref([]);
    
    const onSubmit = (e) => {
      e.preventDefault();
      todos.value.push({
        id: Date.now(),
        subject : todo.value
      })
    }


    return {
      todo,
      todos,
      onSubmit,
    }
  }
}
</script>

<style>
.name{
  color : red;
}
.name1{
  color : green;
}
</style>