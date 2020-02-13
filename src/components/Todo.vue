<template>
  <div class="col-4 mb-4">
    <div class="card">
      <div class="content" v-show="!isEditing">
        <div class="card-header clearfix">
          <div class="float-right">
            <span class="mr-2" v-on:click="editTodo(todo)">
              <i class="fa fa-pencil-square-o" aria-hidden="true"></i>
            </span>
            <span class="mr-2" v-on:click="deleteTodo(todo)">
              <i class="fa fa-trash-o" aria-hidden="true"></i>
            </span>
            <span v-on:click="completeTodo(todo)" v-show="!todo.done">
              <i class="fa fa-check-square-o" aria-hidden="true"></i>
            </span>
          </div>
        </div>

        <div class="card-body">
          <h5 class="card-title">{{ todo.title }}</h5>
          <p class="card-text">{{ todo.project }}</p>
        </div>

        <div class="card-footer text-center">
          <button class='btn btn-success' v-show="todo.done" disabled>
            Completed
          </button>
          <button class='btn btn-secondary' v-show="!todo.done" disabled>
            Pending
          </button>
        </div>
      </div>

      <div class="content" v-show="isEditing">
        <div class="card-body">
          <div class="form-group">
            <label for="title">Title</label>
            <input type="text" class="form-control" v-model="todo.title" id="title">
          </div>
          <div class="form-group">
            <label for="project">Project</label>
            <textarea class="form-control" v-model="todo.project" id="project"></textarea>
          </div>
          <div class="form-group">
            <button class='btn btn-secondary' v-on:click="saveTodo(todo)">
              Save
            </button>
            <button class='btn btn-default' v-on:click="cancelTodo(todo)">
              Cancel
            </button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script type = "text/javascript" >
    export default {
        props: ['todo'],
        data() {
            return {
                isEditing: false,
            };
        },
        methods: {
            editTodo(todo) {
                this._beforeEditingCache = Object.assign({}, todo);
                this.isEditing = true;
            },
            saveTodo(todo) {
                this.isEditing = false;
            },
            cancelTodo(todo) {
                Object.assign(todo, this._beforeEditingCache);
                this.isEditing = false;
            },
            deleteTodo(todo) {
                if (confirm("Are you sure?")) {
                    this.$emit('delete-todo', todo);
                }
            },
            completeTodo(todo) {
                this.$emit('complete-todo', todo);
            },
        },
    }
</script>
<style>
</style>
