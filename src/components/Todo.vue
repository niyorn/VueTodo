<template>
  <div class="container">
    <form @submit.prevent="addTodo">
      <label for="input-todo">Add an item</label>
      <input type="text" name="" id="input-todo" placeholder="Add an item" v-model="todo" autofocus autocomplete="">
      <button type="submit">Add</button>
    </form>

    <ul>
      <transition-group name="todo-items" tag="div">
        <li v-for="(data,index) in todos" :key="index">
          {{ data.todo}}
          <button v-on:click="remove(index)">Delete</button>
        </li>
      </transition-group>
    </ul>

    <p v-if="this.todos.length > 0">You have {{this.todos.length}} items left to do.</p>
    <p v-else>Great job! Everything is done</p>
  </div>
</template>

<script>
  export default {
    name: 'Todo',
    data() {
      return {
        todo: "",
        todos: []
      }
    },
    methods: {
      addTodo() {
        //Check for empty string
        if (this.todo) {
          this.todos.unshift(
            {todo: this.todo});

          this.storeItem();
          this.todo = ""; //reset input-field
        }
      },
      remove(index) {
        this.todos.splice(index, 1);
        this.storeItem();
      },
      storeItem () {
        let data = this.todos;

        localStorage.setItem('Vue-Todo-Items', JSON.stringify(data))
      },
      fetchItem () {
        //Get data from local storage
        let data = JSON.parse(localStorage.getItem("Vue-Todo-Items")|| "[]");

        return data;
      }
    },
    init () {
      //Get all items stored in local storage
      this.todos = this.fetchItem();
    }
  }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  .container {
    display: flex;
    flex-direction: column;
    background-color: #f3f3f3;
    overflow: auto;
    box-shadow: 0 1px 3px rgba(0,0,0,0.12), 0 1px 2px rgba(0,0,0,0.24);
    position: relative;
    z-index: 1;
    height: 100%;
    width: 100%;
  }
  @media only screen and (min-width: 50em) {
    .container {
      max-height: 50em;
      height: 90vh;
      max-width: 37rem;
    }
  }

  ul {
    list-style-type: none;
    width: 100%;
    padding: 2rem;
  }

  ul li {
    padding: 1.2rem;
    padding-right: 4rem;
    font-size: 1.2em;
    border-left: solid 5px rgb(67, 202, 255);
    margin-bottom: 10px;
    background-color: white;
    color: black;
    width: 100%;
    position: relative;
  }

  ul li button {
    position: absolute;
    right: 0;
    height: 100%;
    top: 0;
    border: none;
    width: 5em;
    background-color: #fe7272;
  }

  p {
    text-align: center;
    padding-bottom: 2rem;
    color: grey;
  }

  form {
    display: grid;
    align-items: center;
    width: 100%;
    grid-template-columns: 1fr auto;
    position: sticky;
    z-index: 2;
    top: 0;
    padding: 2rem;
    background-color: black;
  }

  form label{
    position: absolute;
    top: -1000px;
  }

  form input, form button {
    border: none;
    font-size: 1.7em;
    height: 100%;
    box-shadow: 0 14px 28px rgba(0,0,0,0.25), 0 10px 10px rgba(0,0,0,0.22);
  }

  form button {
    background-color: #06e788;
    height: 6rem;
    width: 6rem;
  }

  form input {
    width: 100%;
    color: white;
    background-color: black;
    outline: none;
    padding-left: 0;
    padding-top: 0;
    padding-bottom: 0;
  }
  @media only screen and (min-width: 50em) {
    form input {
      font-size: 3em;
    }
  }
</style>