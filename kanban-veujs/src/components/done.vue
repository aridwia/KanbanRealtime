<template lang="html">
  <div class="">
    <div class="panel panel-primary">
      <div class="panel-heading">
        <h3 class="panel-title">Done</h3>
      </div>
      <div class="panel-body">

        <div class="panel panel-default" v-for="data in datadonedb">
          <div class="panel-heading">{{data.title}}</div>
          <div class="panel-body">
            <label>Point : {{data.point}}</label><br>
            <label>Assigned To : {{data.assignedto}}</label><br>

            <!-- Modal -->
            <button type="button" class="btn btn-info float-right" data-toggle="modal" data-target="#myModal5" @click="getdata(data)">Detail</button>

            <div class="modal fade" role="dialog" id="myModal5">
             <div class="modal-dialog">
               <div class="modal-content">
                 <div class="modal-header">
                   <button type="button" class="close" data-dismiss="modal" aria-hidden="true">&times;</button>
                   <h4 class="modal-title">Detail Task</h4>
                 </div>
                 <div class="modal-body">
                   <label>Title: {{datadone.title}}</label><br>
                   <label>Description : {{datadone.description}}</label><br>
                   <label>Point : {{datadone.point}}</label><br>
                   <label>Assigned To : {{datadone.assignedto}}</label><br>
                 </div>
                 <div class="modal-footer">
                   <button type="button" class="btn btn-danger" data-dismiss="modal" @click="hapusdata(datadone['.key'])">Delete</button>
                   <button type="button" data-dismiss="modal" class="btn btn-warning" @click="pindahDoing(datadone['.key'],datadone.title,datadone.description,datadone.point,datadone.assignedto  )">Doing</button>
                   <button type="button" data-dismiss="modal" class="btn btn-warning" @click="done(datadone['.key'])">Task Done</button>
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
      datadone: {}
    }
  },
  firebase: function () {
    return {
      datadonedb: this.$db.ref('task/done')
    }
  },
  methods: {
    getdata (datadonedb) {
      this.datadone = datadonedb
    },
    hapusdata (id) {
      this.$db.ref('task/done/' + id).remove()
    },
    pindahDoing (id, title, description, point, assign) {
      this.$db.ref('task/doing').push({
        title: title,
        description: description,
        point: point,
        assignedto: assign,
        status: 'doing'
      })
      this.$db.ref('task/done/' + id).remove()
    },
    done (id) {
      this.$db.ref('task/done/' + id).remove()
    }
  }
}
</script>

<style lang="css">
</style>
