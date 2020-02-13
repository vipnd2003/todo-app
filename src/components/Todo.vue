<template>
  <div class="col-4 mb-4">
    <div class="card">
      <div class="content" v-show="!isEditing">
        <div class="card-header clearfix" v-bind:class="{ 'bg-danger' : dueSoon }">
          <div class="float-right">
            <span class="mr-2" v-on:click="editTodo(todo)">
              <i class="fa fa-pencil-square-o" aria-hidden="true"></i>
            </span>
            <span class="mr-2" v-on:click="deleteTodo(todo)">
              <i class="fa fa-trash-o" aria-hidden="true"></i>
            </span>
            <span v-on:click="completeTodo(todo)" v-show="!todo.status">
              <i class="fa fa-check-square-o" aria-hidden="true"></i>
            </span>
          </div>
        </div>

        <div class="card-body">
          <h5 class="card-title">{{ todo.title }}</h5>
          <p class="card-text">{{ todo.description }}</p>
          <p class="card-text font-weight-bold" v-bind:class="{ 'text-danger' : dueSoon }">{{ todo.deadline }}</p>
        </div>

        <div class="card-footer text-center">
          <button class='btn btn-success' v-show="todo.status" disabled>
            Completed
          </button>
          <button class='btn btn-secondary' v-show="!todo.status" disabled>
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
            <label for="description">Description</label>
            <textarea class="form-control" v-model="todo.description" id="description"></textarea>
          </div>
          <div class="form-group">
            <label for="deadline">Deadline</label>
            <input type="date" class="form-control" v-model="todo.deadline" id="deadline">
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
        computed: {
            dueSoon: function () {
                let now = new Date();
                let deadline = new Date(this.todo.deadline);

                if (!this.todo.status) {
                    return deadline < now;
                }

                return false;
            }
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
