<template lang="html">
  <div class="">
    <div class="panel panel-danger">
      <div class="panel-heading">Back Log</div>
      <div class="panel-body">
        <div class="panel panel-default" v-for="data in log">
          <div class="panel-heading">
            <h3 class="panel-title">{{data.title}}</h3>
          </div>
          <div class="panel-body">
            <label>Point : {{data.point}}</label><br>
            <label>Assigned To : {{data.assignedto}}</label><br>
            <!-- <div class="rows"> -->
               <button type="button" class="btn btn-info float-right" data-toggle="modal" data-target="#myModal2" @click="getdata(data)">Detail</button>

               <div class="modal fade" role="dialog" id="myModal2">
                <div class="modal-dialog">
                  <div class="modal-content">
                    <div class="modal-header">
                      <button type="button" class="close" data-dismiss="modal" aria-hidden="true">&times;</button>
                      <h4 class="modal-title">Detail Task</h4>
                    </div>
                    <div class="modal-body">
                      <label>Title: {{alltask.title}}</label><br>
                      <label>Description : {{alltask.description}}</label><br>
                      <label>Point : {{alltask.point}}</label><br>
                      <label>Assigned To : {{alltask.assignedto}}</label><br>
                    </div>
                    <div class="modal-footer">
                      <button type="button" class="btn btn-danger" data-dismiss="modal" @click="hapusdata(alltask['.key'])">Delete</button>
                      <button type="button" class="btn btn-warning" @click="pindahToDo(alltask['.key'],alltask.title,alltask.description,alltask.point,alltask.assignedto  )">To Do</button>
                    </div>
                  </div>
                </div>
              </div>

            <!-- </div> -->
          </div>
        </div>
      </div>
      </div>

  </div>
</template>

<script>
export default {
  data () {
    return {
      alltask: {}
    }
  },
  firebase: function () {
    return {
      log: this.$db.ref('task/log')
    }
  },
  methods: {
    getdata (log) {
      console.log('data log ', log)
      this.alltask = log
    },
    hapusdata (id) {
      this.$db.ref('task/log/' + id).remove()
    },
    pindahToDo (id, title, description, point, assign) {
      this.$db.ref('task/todo').push({
        title: title,
        description: description,
        point: point,
        assignedto: assign,
        status: 'todo'
      })
      this.$db.ref('task/log/' + id).remove()
    }
  }
}
</script>

<style lang="css">
</style>
