<template>
    <input 
      type="text" 
      v-model = "name"
    >
    <button 
      class = "btn btn-primary"
      @click="onSubmit()"
    >
    클릭
    </button>
</template>

<script>
import { ref } from 'vue';
export default {
  setup(){
    const name = ref('Soko coder');
    
    const onSubmit = () => {
      console.log(name.value)
    }


    return {
      name,
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