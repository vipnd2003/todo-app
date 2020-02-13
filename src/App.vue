<template>
  <div id="app">
      <todo-list v-bind:todos="todos"></todo-list>
  </div>
</template>

<script>
import TodoList from './components/TodoList';

export default {
    name: 'App',
    components: {
        TodoList,
    },
    data() {
        return {
            todos: [{
                title: 'Todo A',
                description: 'Project A',
                deadline: '2020-02-12',
                status: false,
            }, {
                title: 'Todo B',
                description: 'Project B',
                deadline: '2020-02-12',
                status: true,
            }, {
                title: 'Todo C',
                description: 'Project C',
                deadline: '2020-02-14',
                status: false,
            }, {
                title: 'Todo D',
                description: 'Project D',
                deadline: '2020-02-14',
                status: true,
            }],
        };
    }
}
</script>
