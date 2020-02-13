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
              <label for="description">Description</label>
              <textarea v-model="descriptionText" class="form-control" id="description"></textarea>
            </div>
            <div class="form-group">
              <label for="deadline">Deadline</label>
              <input v-model="deadlineText" type="date" class="form-control"  id="deadline">
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
                descriptionText: '',
                deadlineText: '',
            };
        },
        methods: {
            saveTodo() {
                if (this.titleText.length > 0 && this.descriptionText.length > 0) {
                    const title = this.titleText;
                    const description = this.descriptionText;
                    const deadline = this.deadlineText;
                    this.$emit('create-todo', {
                        title,
                        description,
                        deadline,
                        status: false,
                    });

                    this.titleText = '';
                    this.descriptionText = '';
                    this.deadlineText = '';

                    $('#create-todo').modal('hide');
                } else {
                    alert('Please input title and project.');
                }
            },
        },
    };
</script>
