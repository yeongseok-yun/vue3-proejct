<template>
    
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
            v-value = "todo.completed"  
            @change="toggleTodo(index)"
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
            @click = "deleteTodo(index)"
            >
            삭제
          </button>
        </div>
      </div>
    </div>
</template>

<script>
export default {
    props:{
        todos:{
            type : Array,
            required : true
        }
    },
    emits: ['toggle-todo','delete-todo'],
    setup(props,{ emit }){
        const toggleTodo = (index) => {
            emit('toggle-todo',index);
        }
        const deleteTodo = (index) => {
            emit('delete-todo',index);
        }
        return {
            toggleTodo,
            deleteTodo
        }
    }
}
</script>

<style>

</style>