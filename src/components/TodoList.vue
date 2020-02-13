<template>
  <div class="container">
    <div class="text-center mt-3">
      <button class="btn btn-primary" v-on:click="todoFilterKey = 'all'">All: {{todos.length}}</button>
      <button class="btn btn-success" v-on:click="todoFilterKey = 'completed'">Completed Tasks: {{todos.filter(todo => {return todo.status === true}).length}}</button>
      <button class="btn btn-secondary" v-on:click="todoFilterKey = 'pending'">Pending Tasks: {{todos.filter(todo => {return todo.status === false}).length}}</button>
    </div>

    <hr>

    <div class="row">
      <todo v-on:delete-todo="deleteTodo" v-on:complete-todo="completeTodo" v-for="todo in todoFilter" v-bind:todo="todo"></todo>
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
        data() {
            return {
                todoFilterKey: 'all',
            }
        },
        components: {
            Todo,
            CreateTodo
        },
        computed: {
            todoFilter() {
                return this[this.todoFilterKey];
            },
            all() {
                return this.todos;
            },
            completed() {
                return this.todos.filter(todo => {return todo.status === true});
            },
            pending() {
                return this.todos.filter(todo => {return todo.status === false});
            }
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
                this.todos[todoIndex].status = true;
            },
        },
    }
</script>
<style>
</style>
