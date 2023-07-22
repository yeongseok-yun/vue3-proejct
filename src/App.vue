<template>
    <div class="name">
      {{name}}
    </div>
    <button 
      class = "btn btn-primary"
      @click="consoleLog(name)"
    >
    클릭
    </button>
</template>

<script>
export default {
  setup(){
    const name = 'Soko coder'

    // const greeting = (name) => {
    //   return 'Hello, ' + name;
    // };
    const consoleLog = (msg) => {
      console.log(msg)
    }
    return {
      name,
      consoleLog
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