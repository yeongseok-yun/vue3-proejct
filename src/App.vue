<template>
  <div class="container">
    <h4>count : {{ count }}</h4>
    <h4>count : {{ doubleCountComputed }}</h4>
    <h4>count : {{ doubleCountComputed }}</h4>
    <h4>count : {{ doubleCountMethod() }}</h4>
    <h4>count : {{ doubleCountMethod() }}</h4>
    <button @click = "count++">Add one</button>
    <h2>To-Do List</h2>
    <TodoSimpleForm @add-todo="addTodo" />
    
    <div v-if="!todos.length">
      저장된 Todo가 없습니다.
    </div>
    <TodoList :todos="todos" 
      @toggle-todo = "toggleTodo" 
      @delete-todo = "deleteTodo"
    />
  </div>
</template>

<script>
import { ref , computed} from 'vue';
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
    
    const toggleTodo = (index) =>{
      todos.value[index].completed = !todos.value[index].completed;
    }
    const deleteTodo = (index) => {
      todos.value.splice(index,1);

    }
    const count = ref(1);
    //computed는 변수 활용 불가
    //computed는 한번 계산후 값을 저장, 변수처럼 활용이 되는듯.
    const doubleCountComputed = computed(() =>{
      console.log('computed')
      return count.value * 2 ;
    })

    const doubleCountMethod = () => {
      console.log('method')
      return count.value * 2 ;
    }
    return {
      todos,
      addTodo,
      toggleTodo,
      deleteTodo,
      count,
      doubleCountComputed,
      doubleCountMethod,
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