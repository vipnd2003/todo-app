<template>
  <div class="container">
    <div class="text-center mt-3">
      <span class="badge badge-success">Completed Tasks: {{todos.filter(todo => {return todo.done === true}).length}}</span>
      <span class="badge badge-secondary">Pending Tasks: {{todos.filter(todo => {return todo.done === false}).length}}</span>
    </div>

    <hr>

    <div class="row">
      <todo v-on:delete-todo="deleteTodo" v-on:complete-todo="completeTodo" v-for="todo in todos" v-bind:todo="todo"></todo>
    </div>

    <hr>

    <create-todo v-on:create-todo="createTodo"></create-todo>
  </div>
</template>

<script type = "text/javascript" >
    import Todo from './Todo';
    import CreateTodo from "./CreateTodo";

    export default {
        props: ['todos'],
        components: {
            Todo,
            CreateTodo
        },
        methods: {
            deleteTodo(todo) {
                const todoIndex = this.todos.indexOf(todo);
                this.todos.splice(todoIndex, 1);
            },
            createTodo(todo) {
                this.todos.push(todo);
            },
            completeTodo(todo) {
                const todoIndex = this.todos.indexOf(todo);
                this.todos[todoIndex].done = true;
            },
        },
    }
</script>
<style>
</style>
