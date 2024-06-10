<template>
  <div id="app">
    <TodoApp />
  </div>
</template>

<script>
import TodoApp from './components/TodoApp.vue';

export default {
  components: {
    TodoApp
  }
};
</script>

<style>
body {
  font-family: 'Roboto', sans-serif;
  margin: 0;
  background-image: url(/src/assets/bgbru.jpg); 
}

#app {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
}
</style>
