<template>
  <div>
    <button type="button" class="btn btn-primary" data-toggle="modal" data-target="#create-todo">
      Create Todo
    </button>
    <div class="modal fade" id="create-todo" tabindex="-1" role="dialog" aria-labelledby="exampleModalLabel" aria-hidden="true">
      <div class="modal-dialog" role="document">
        <div class="modal-content">
          <div class="modal-header">
            <h5 class="modal-title" id="exampleModalLabel">Create Todo</h5>
            <button type="button" class="close" data-dismiss="modal" aria-label="Close">
              <span aria-hidden="true">&times;</span>
            </button>
          </div>
          <div class="modal-body">
            <div class="form-group">
              <label for="title">Title</label>
              <input v-model="titleText" type="text" class="form-control" id="title">
            </div>
            <div class="form-group">
              <label for="project">Project</label>
              <textarea v-model="projectText" class="form-control" id="project"></textarea>
            </div>
          </div>
          <div class="modal-footer">
            <button type="button" class="btn btn-secondary" data-dismiss="modal">Close</button>
            <button type="button" class="btn btn-primary" v-on:click="saveTodo()">Save changes</button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
    export default {
        data() {
            return {
                titleText: '',
                projectText: '',
            };
        },
        methods: {
            saveTodo() {
                if (this.titleText.length > 0 && this.projectText.length > 0) {
                    const title = this.titleText;
                    const project = this.projectText;
                    this.$emit('create-todo', {
                        title,
                        project,
                        done: false,
                    });

                    this.titleText = '';
                    this.projectText = '';

                    $('#create-todo').modal('hide');
                } else {
                    alert('Please input title and project.');
                }
            },
        },
    };
</script>
