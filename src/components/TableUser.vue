<template>   

    <table class="table table-bordered table-hover">
      <thead class="thead-dark">
        <tr>
          <th scope="col">DNI</th>
          <th scope="col">Nombre</th>
          <th scope="col">Apellido</th>
          <th scope="col">Fecha de nacimiento</th>
          <th scope="col">Email</th>
          <th scope="col">Contra</th>
          <th scope="col">Acciones</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="alumno in alumnos">
          <td>{{ alumno.dni_alumno}}</td>
          <td>{{ alumno.nombre}}</td>
          <td>{{ alumno.apellido}}</td>
          <td>{{ alumno.fecha_nacimiento }}</td>
          <td>{{alumno.email  }}</td>
          <td>******</td>
          <td class="table-action-cell">
            <div class="d-flex align-items-center justify-content-center">
              <div class="mr-2">
                <a type="button" class="btn btn-success" :href="`/encargado/editar/`">
                  <i class="fas fa-edit"></i>
                </a>
              </div>
              <div>
                <button v-on:click='deleteAlumno(alumno)' class="btn btn-danger">
                  <i class="far fa-trash-alt"></i>
                </button>
              </div>
            </div>
          </td>
        </tr>
      </tbody>
    </table>


</template>

<script>
import axios from 'axios'
export default {
  data() {
    return {
      alumnos : [],
      postURL: 'http://127.0.0.1:5000'      
    };
  },
  methods: {
    deleteAlumno(alumno) {
      var config_request = {
        headers: {
          'Content-Type': 'application/json',
          'Access-Control-Allow-Origin': '*'
        }
      };

      console.log(alumno.dni_alumno);

      axios.delete(this.postURL + '/alumno', { 
          data: { "dni_alumno": alumno.dni_alumno },
          ...config_request
        })
        .then(res => {                      
          this.alumnos.splice(this.alumnos.indexOf(alumno), 1);
          console.log(res.data);              
        })
        .catch((error) => {
          console.log(error);
        }); 
    }
  },
  created(){ 
      //with axios
      axios.post(this.postURL + '/alumnos')
        .then((res) => {  
            this.alumnos = res.data;
        })
        .catch((error) => {
            console.log(error)
        })
  }
};
</script>

<style>
@import url('https://cdnjs.cloudflare.com/ajax/libs/twitter-bootstrap/4.5.2/css/bootstrap.css');
@import url('https://cdnjs.cloudflare.com/ajax/libs/font-awesome/5.15.4/css/all.min.css');
</style>
