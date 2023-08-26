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
    <hr />
    <div class = "row justify-content-center">
      <nav aria-label="Page navigation example">
        <ul class="pagination">
          <li v-if="currentPage !==1" class="page-item">
            <a 
              class="page-link" 
              @click = "getTodos(currentPage - 1)"
              style = "cursor:pointer"
            >Previous
            </a>
          </li>
          
          <li
            v-for="page in numberOfPages" 
            :key="page"
            class="page-item"
            :class="currentPage === page ? 'active' : ''"
          >
            <a 
              class="page-link" 
              @click = "getTodos(page)"
              style = "cursor:pointer"
            >{{ page }}</a>
          </li>
          
          <li v-if="numberOfPages !== currentPage" class="page-item">
            <a 
              class="page-link" 
              href="#"
              @click = "getTodos(currentPage + 1)"
              style = "cursor:pointer"
            >Next
            </a>
          </li>
        </ul>
      </nav>
    </div>
  </div>

</template>

<script>
import { ref, computed, watch, reactive } from 'vue';
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
    const numberOfTodos = ref(0);
    const limit = 5;
    const currentPage = ref(1);
    const a = reactive({
      b:1,
      c:3
    })
    watch(() => [a.b,a.c],(current,prev)=>{
      console.log(current,prev)
    })
    a.b =2;
    watch([currentPage, numberOfTodos],(currentPage,prev)=> {
      console.log(currentPage,prev)
    })
    const numberOfPages = computed(() =>{
      return Math.ceil(numberOfTodos.value/limit);
    });


    const getTodos = async (page = currentPage.value) => {
      try {
        const res =await axios.get(
          `http://localhost:3000/todos?_page=${page}&_limit=${limit}`
        );  
        currentPage.value = page
        numberOfTodos.value = res.headers['x-total-count']
        todos.value = res.data
      } catch (err) {
        error.value = '예기치 못한 에러가 발생했습니다.'
      }
    }

    getTodos();

    const addTodo = async (todo) =>{
      console.log(todo)
      //db 저장
      error.value = '';
      try {
        const res = await axios.post('http://localhost:3000/todos',{
          subject : todo.subject,
          completed : todo.completed,
        })  
        todos.value.push(res.data);
      } catch (err) {
        error.value = '예기치 못한 에러가 발생했습니다.'
      }
      
      // .then(res =>{
      //   console.log(res);
      //   todos.value.push(res.data);
      // }).catch(err => {
      //   console.log(err);
      //   error.value = '예기치 못한 에러가 발생했습니다.'
      // });
      
    }
    
    const toggleTodo = async (index) =>{
      error.value = ''
      const id = todos.value[index].id;
      try {
        await axios.patch('http://localhost:3000/todos/' + id,{
          completed : !todos.value[index].completed
        });
        todos.value[index].completed = !todos.value[index].completed;  
      } catch (error) {
        error.value = '예기치 못한 에러가 발생했습니다.'
      }
      
    }
    const deleteTodo = async (index) => {
      error.value = ''
      const id = todos.value[index].id;
      try {
        await axios.delete('http://localhost:3000/todos/' + id);  
        todos.value.splice(index,1);
      } catch (err) {
        error.value = '예기치 못한 에러가 발생했습니다.'
      }
      
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
      numberOfPages,
      currentPage,
      getTodos,
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