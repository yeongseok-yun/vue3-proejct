<template>
    <div class="name">
      {{name}}
      <!--함수호출-->
      {{greeting(name) }}
    </div>
    <div>Hi</div>
</template>

<script>
export default {
  setup(){
    const name = 'Soko coder'

    const greeting = (name) => {
      return 'Hello, ' + name;
    };

    return {
      name
      ,greeting
    }
  }
}
</script>

<style>
.name{
  color : red;
}
</style>