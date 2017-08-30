<template>
  <div>
    <!--<ul>-->
      <!--<li> Todo A </li>-->
      <!--<li> Todo B </li>-->
      <!--<li> Todo C </li>-->
    <!--</ul>-->
    <p>Completed Tasks: {{todos.filter(todo => {return todo.done === true}).length}}</p>
    <p>Pending Tasks: {{todos.filter(todo => {return todo.done === false}).length}}</p>
0
    <todo v-bind:key="i" v-on:delete-todo="deleteTodo(todo)" v-on:complete-todo="completeTodo(todo)" v-for="(todo, i) in todos" v-bind:todo="todo"></todo>
    <create-todo v-on:create-todo="createTodo(reaction)" :reaction="reaction"></create-todo>

  </div>
</template>

<script type="text/javascript">

  import Todo from "./Todo"
  import CreateTodo from "./CreateTodo"

  export default {
    props: ['todos'],

    components: {
      Todo,
      CreateTodo,
    },

    data() {
      return{
        reaction:{title:"", project:"", done:false}
      }
    },

    methods: {
      deleteTodo(todo) {
        const todoIndex = this.todos.indexOf(todo);
        this.todos.splice(todoIndex, 1);
      },
      completeTodo(todo) {
        const todoIndex = this.todos.indexOf(todo);
        console.log(todo);
//        this.$set(this.todos[todoIndex], "done", true);
        this.todos[todoIndex].done = true;
      },
      createTodo(todo) {
        this.todos.push(todo);
        this.reaction = {title:"", project:"", done:false};
      },
    },
  };
</script>

<style>
</style>
