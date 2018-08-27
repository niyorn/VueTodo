<template>
  <div id="app">
    <Todo/>
  </div>
</template>

<script>
  import Todo from './components/Todo.vue'

  export default {
    name: 'app',
    components: {
      Todo
    }
  }
</script>

<style>
  * {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
  }

  html,body{
    height: 100%;
    font-family: sans-serif;
  }

  #app {
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100%;
    background-color: #00ddb4;
    position: relative;
  }
  @media(min-width: 50em) {
    #app::after {
    content: "";
    height: 45rem;
    width: 45rem;
    position: absolute;
    background-color: #72727233;
    border-radius: 50%;
  }
  }

  button:hover {
    cursor: pointer;
  }

</style>