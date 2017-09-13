<template lang="html">
  <div class="">

    <navbar></navbar>
    <!-- Trigger the modal with a button -->
      <div class="rows">
         <button type="button" class="btn btn-info float-right" data-toggle="modal" data-target="#myModal">New Task</button>
      </div><br>

      <div class="rows">
    <!-- Modal -->
        <div class="modal fade" role="dialog" id="myModal">
          <div class="modal-dialog">
    <!-- Modal content-->
            <div class="modal-content">
              <div class="modal-header">
                <button type="button" class="close" data-dismiss="modal" aria-hidden="true">&times;</button>
                <h4 class="modal-title">New Task</h4>
              </div>

              <div class="modal-body">
                <div class="form-group">
                  <label class="control-label" for="focusedInput">Title</label>
                  <input class="form-control" type="text" v-model="title" id="focusedInput">
                  <!-- <p>{{title}}</p> -->
                </div>
                <div class="form-group">
                  <label class="control-label" for="focusedInput">Description</label>
                  <input class="form-control" v-model="description" type="text" id="focusedInput">
                  <!-- <p>{{description}}</p> -->
                </div>
                <div class="form-group">
                  <label class="control-label" for="focusedInput">Point</label>
                  <input class="form-control" type="text" v-model="point" id="focusedInput">
                  <!-- <p>{{point}}</p> -->
                </div>
                <div class="form-group">
                  <label class="control-label" for="focusedInput">Assigned to</label>
                  <input class="form-control" type="text" v-model="assignedto" id="focusedInput">
                  <!-- <p>{{assignedto}}</p> -->
                </div>
              </div>

              <div class="modal-footer">
                <button type="button" class="btn btn-default" data-dismiss="modal">Close</button>
                <button type="button" class="btn btn-primary" data-dismiss="modal" @click="addtask">Add</button>
              </div>
            </div>
          </div>
        </div>
      </div>

      <div class="rows">
        <div class="col-md-3">
          <backlog></backlog>
        </div>

        <div class="col-md-3">
          <todo></todo>
        </div>

        <div class="col-md-3">
          <doing></doing>
        </div>

        <div class="col-md-3">
          <done></done>
        </div>
      </div>

  </div>
</template>

<script>
import navbar from '@/components/navbar'
import backlog from '@/components/backlog'
import todo from '@/components/todo'
import doing from '@/components/doing'
import done from '@/components/done'

export default {
  data () {
    return {
      title: '',
      description: '',
      point: '',
      assignedto: ''
    }
  },
  components: {
    navbar,
    backlog,
    todo,
    doing,
    done
  },
  methods: {
    addtask () {
      this.$db.ref('task/log/').push({
        title: this.title,
        description: this.description,
        point: this.point,
        assignedto: this.assignedto,
        status: 'back-log'
      })
      this.title = ''
      this.description = ''
      this.point = ''
      this.assignedto = ''
    }
  }
}
</script>

<style lang="css">
</style>
