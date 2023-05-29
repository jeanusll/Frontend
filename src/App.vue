<template>
  <div id="app">    
    <div class="container">
      <CreateAlumno/>
      <TableUser/>
      <!--<UpdateUser/>-->
    </div>

  </div>
</template>

<script>
import TableUser from './components/TableUser.vue'
import UpdateUser from './components/UpdateUser.vue'
import CreateAlumno from './components/CreateAlumno.vue'

export default {
  name: 'App',
  components: {
    UpdateUser,
    TableUser,
    CreateAlumno
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
