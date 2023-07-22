<template>
    <div class="name">
      {{name}}
    </div>
    <input type="text" :value = name>
    <button 
      class = "btn btn-primary"
      @click="updateName()"
    >
    클릭
    </button>
</template>

<script>
import { ref } from 'vue';
export default {
  setup(){
    const name = ref('Soko coder');

    // const greeting = (name) => {
    //   return 'Hello, ' + name;
    // };
    const updateName = () => {
      name.value = 'Soko coder1'
      console.log(name)
    }
    return {
      name,
      updateName
    //  ,greeting
    }
  }
}
</script>

<style>
.name{
  color : red;
}
</style>