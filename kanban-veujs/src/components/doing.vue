<template lang="html">
  <div class="">
    <div class="panel panel-success">
      <div class="panel-heading">
        <h3 class="panel-title">Doing</h3>
      </div>
      <div class="panel-body">

        <div class="panel panel-default" v-for="data in datadoingdb">
          <div class="panel-heading">{{data.title}}</div>
          <div class="panel-body">

            <label>Point : {{data.point}}</label><br>
            <label>Assigned To : {{data.assignedto}}</label><br>

            <!-- Modal -->
            <button type="button" class="btn btn-info float-right" data-toggle="modal" data-target="#myModal4" @click="getdata(data)">Detail</button>

            <div class="modal fade" role="dialog" id="myModal4">
             <div class="modal-dialog">
               <div class="modal-content">
                 <div class="modal-header">
                   <button type="button" class="close" data-dismiss="modal" aria-hidden="true">&times;</button>
                   <h4 class="modal-title">Detail Task</h4>
                 </div>
                 <div class="modal-body">
                   <label>Title: {{datadoing.title}}</label><br>
                   <label>Description : {{datadoing.description}}</label><br>
                   <label>Point : {{datadoing.point}}</label><br>
                   <label>Assigned To : {{datadoing.assignedto}}</label><br>
                 </div>
                 <div class="modal-footer">
                   <button type="button" class="btn btn-danger" data-dismiss="modal" @click="hapusdata(datadoing['.key'])">Delete</button>
                   <button type="button" class="btn btn-warning" @click="pindahToDo(datadoing['.key'],datadoing.title,datadoing.description,datadoing.point,datadoing.assignedto  )">To DO</button>
                   <button type="button" class="btn btn-warning" @click="pindahDone(datadoing['.key'],datadoing.title,datadoing.description,datadoing.point,datadoing.assignedto  )">Done</button>
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
      datadoing: {}
    }
  },
  firebase: function () {
    return {
      datadoingdb: this.$db.ref('task/doing')
    }
  },
  methods: {
    getdata (datadoingdb) {
      console.log('datadoingdb', datadoingdb)
      this.datadoing = datadoingdb
      console.log('datadoing', this.datadoing)
    },
    hapusdata (id) {
      this.$db.ref('task/doing/' + id).remove()
    },
    pindahDone (id, title, description, point, assign) {
      this.$db.ref('task/done').push({
        title: title,
        description: description,
        point: point,
        assignedto: assign,
        status: 'done'
      })
      this.$db.ref('task/doing/' + id).remove()
    },
    pindahToDo (id, title, description, point, assign) {
      this.$db.ref('task/todo').push({
        title: title,
        description: description,
        point: point,
        assignedto: assign,
        status: 'todo'
      })
      this.$db.ref('task/doing/' + id).remove()
    }
  }

}
</script>

<style lang="css">
</style>
