<template lang="html">
  <div class="">
    <div class="panel panel-warning">
      <div class="panel-heading">
        <h3 class="panel-title">To Do</h3>
      </div>
      <div class="panel-body">

        <div class="panel panel-default" v-for="data in datatododb">
          <div class="panel-heading">{{data.title}}</div>
          <div class="panel-body">
            <label>Point : {{data.point}}</label><br>
            <label>Assigned To : {{data.assignedto}}</label><br>

            <!-- Modal -->
            <button type="button" class="btn btn-info float-right" data-toggle="modal" data-target="#myModal3" @click="getdata(data)">Detail</button>

            <div class="modal fade" role="dialog" id="myModal3">
             <div class="modal-dialog">
               <div class="modal-content">
                 <div class="modal-header">
                   <button type="button" class="close" data-dismiss="modal" aria-hidden="true">&times;</button>
                   <h4 class="modal-title">Detail Task</h4>
                 </div>
                 <div class="modal-body">
                   <label>Title: {{datatodo.title}}</label><br>
                   <label>Description : {{datatodo.description}}</label><br>
                   <label>Point : {{datatodo.point}}</label><br>
                   <label>Assigned To : {{datatodo.assignedto}}</label><br>
                 </div>
                 <div class="modal-footer">
                   <button type="button" class="btn btn-danger" data-dismiss="modal" @click="hapusdata(datatodo['.key'])">Delete</button>
                   <button type="button" class="btn btn-warning" @click="pindahBackLog(datatodo['.key'],datatodo.title,datatodo.description,datatodo.point,datatodo.assignedto  )">Back Log</button>
                   <button type="button" class="btn btn-warning" @click="pindahDoing(datatodo['.key'],datatodo.title,datatodo.description,datatodo.point,datatodo.assignedto  )">Doing</button>
                 </div>
               </div>
             </div>
           </div>

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
      datatodo: {}
    }
  },
  firebase: function () {
    return {
      datatododb: this.$db.ref('task/todo')
    }
  },
  methods: {
    getdata (datatododb) {
      console.log('datatododb', datatododb)
      this.datatodo = datatododb
    },
    hapusdata (id) {
      this.$db.ref('task/todo/' + id).remove()
    },
    pindahDoing (id, title, description, point, assign) {
      this.$db.ref('task/doing').push({
        title: title,
        description: description,
        point: point,
        assignedto: assign,
        status: 'doing'
      })
      this.$db.ref('task/todo/' + id).remove()
    },
    pindahBackLog (id, title, description, point, assign) {
      this.$db.ref('task/log').push({
        title: title,
        description: description,
        point: point,
        assignedto: assign,
        status: 'todo'
      })
      this.$db.ref('task/todo/' + id).remove()
    }
  }
}
</script>

<style lang="css">
</style>
