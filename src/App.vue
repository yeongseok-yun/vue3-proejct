<template>
  <nav class="navbar navbar-expand-lg navbar-light bg-light">
  <router-link class="navbar-brand" :to="{name : 'Home'}">
    YuN
  </router-link>

  <ul class="navbar-nav mr-auto">
    <li class="nav-item active">
      <router-link class="nav-link" :to="{name : 'Todos'}">
        Todos <span class="sr-only">(current)</span>
      </router-link>
    </li>
  </ul>
</nav>
  <router-view/>
</template>

<script>
export default {
}
</script>

<style>
</style>