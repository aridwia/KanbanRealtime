<template lang="html">
  <div class="">
    <div class="panel panel-default">
      <div class="panel-heading"></div>
      <div class="panel-body">
        Panel content
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
    getdata(log){
      console.log('data log ',log);
      this.alltask = log
    }
  }
}
</script>

<style lang="css">
</style>
