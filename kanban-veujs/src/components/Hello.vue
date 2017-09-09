<template>
  <div class="hello">
    

    <div class="container">
      <div class="row">

        <div class="col-md-3">
          <div class="panel panel-primary" >
            <div class="panel-heading">
              <h3 class="panel-title">Panel primary</h3>
            </div>
            <div class="panel-body">
              Panel content
            </div>
          </div>
        </div>

        <div class="col-md-3">
          <div class="panel panel-success">
            <div class="panel-heading">
              <h3 class="panel-title">Panel success</h3>
            </div>
            <div class="panel-body">
              Panel content
            </div>
          </div>
        </div>

        <div class="col-md-3">
          <div class="panel panel-warning">
            <div class="panel-heading">
              <h3 class="panel-title">Panel warning</h3>
            </div>
            <div class="panel-body">
              Panel content
            </div>
          </div>
        </div>

        <div class="col-md-3">
          <div class="panel panel-danger">
            <div class="panel-heading">
              <h3 class="panel-title">Panel danger</h3>
            </div>
            <div class="panel-body">
              Panel content
            </div>
          </div>
        </div>

    </div>
  </div>
</div>
</template>

<script>
export default {
  name: 'hello',
  data () {
    return {
      msg: 'Welcome to Your Vue.js App'
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1, h2 {
  font-weight: normal;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: inline-block;
  margin: 0 10px;
}

a {
  color: #42b983;
}
</style>
