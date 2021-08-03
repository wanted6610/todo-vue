<template>
  <div id="app">
    <div class="container">
      <div class="todo-wrapper">
        <h2 class="todo-title">Todo Список</h2>
        <TodoList />
      </div>
    </div>
  </div>
</template>

<script>
import TodoList from './components/TodoList';

export default {
  name: 'App',
  components: {
    TodoList,
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin-top: 60px;
}
  *{
    box-sizing: border-box;
  }
  .container{
    display: flex;
    justify-content: center;
    padding: 0 20px;
  }
  .todo-wrapper{
    width: 600px;
    padding: 20px;
    border-radius: 6px;
    -webkit-box-shadow: 4px 4px 8px 0px rgba(34, 60, 80, 0.2);
    -moz-box-shadow: 4px 4px 8px 0px rgba(34, 60, 80, 0.2);
    box-shadow: 4px 4px 8px 0px rgba(34, 60, 80, 0.2);
  }
  .todo-title{
    text-align: center;
  }
</style>
