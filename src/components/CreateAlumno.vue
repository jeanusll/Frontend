<template>
    <div>
        <div class="row mt-5 mb-4">
        <div class="col-2 mt-4">
          <h3>Alumnos</h3>
        </div>   
        <div class="col-2 mt-4 offset-8">
          <button type="button" class="btn btn-success" @click="openModal">
            Añadir
            <i class="fas fa-plus"></i>
          </button>
        </div>  

      </div>
      <!-- Ventana modal -->
      <div class="modal" tabindex="-1" role="dialog" :class="{ 'show': showModal }">
        <div class="modal-dialog" role="document">
          <div class="modal-content">
            <!-- Contenido de la ventana modal -->
            <div class="modal-header">
              <h5 class="modal-title ">Agregar Alumno</h5>
              <button type="button" class="close" @click="closeModal">
                <span aria-hidden="true">&times;</span>
              </button>
            </div>
            <div class="modal-body">
              <form v-on:submit='addAlumno'>
                <div class="form-group ">
                  <label for="dni">DNI</label>
                  <input
                    required
                    type="text"
                    v-model="newAlumno.dni_alumno"
                    placeholder="Ej: 74521563"
                    pattern="^[0-9]{8}$"
                    class="form-control"
                  />
                </div>
                <div class="form-group">
                  <label for="nombre">Nombre</label>
                  <input
                    required
                    type="text"
                    v-model="newAlumno.nombre"
                    class="form-control"
                  />
                </div>                
                <div class="form-group ">
                  <label for="dni">Apellidos</label>
                  <input
                    required
                    type="text"
                    v-model="newAlumno.apellido"
                    class="form-control"
                  />
                </div>
                <div class="form-group ">
                  <label for="fecha_nacimiento">Fecha de Nacimiento</label>
                  <input
                    required
                    type="date"
                    v-model="newAlumno.fecha_nacimiento"
                    class="form-control"
                  />
                </div>
                <div class="form-group ">
                  <label for="foto">foto</label>
                  <input
                    required
                    type="text"
                    v-model="newAlumno.foto"
                    class="form-control"
                  />
                </div>
                <div class="form-group ">
                  <label for="id_grupo_usuario">Grupo Usuario</label>
                  <input
                    required
                    type="number"
                    v-model="newUsuario.id_grupo_usuario"
                    placeholder="1"
                    class="form-control"
                  />
                </div>
                <div class="form-group ">
                  <label for="email">Email</label>
                  <input
                    required
                    type="email"
                    v-model="newUsuario.email"
                    placeholder="juan@gmail.com"
                    class="form-control"
                  />
                </div>
                <div class="form-group ">
                  <label for="contra">Contraseña</label>
                  <input
                    required
                    type="password"
                    v-model="newUsuario.contra"
                    class="form-control"
                  />
                </div>
                <button type="submit" class="btn btn-primary">Guardar</button>
              </form>
              <button type="button" class="btn btn-secondary" @click="closeModal">Cerrar</button>
            </div>
          </div>
        </div>
      </div>
    </div>
  </template>
  
  <script>
  import axios from 'axios'
  export default {
    data() {
      return {        
        newAlumno: {},
        newUsuario: {},
        postURL: 'http://localhost:5000',
        showModal: false
      };
    },
    methods: {
      openModal() {
        this.showModal = true;
      },
      closeModal() {
        this.showModal = false;
      },
      addAlumno(e) {
        e.preventDefault();

        var config_request = {
          headers: {
            'Content-Type': 'application/json',
            'Access-Control-Allow-Origin': '*'
          }
        };

        axios.put(this.postURL + '/usuario', this.newUsuario, config_request)
          .then(resUsuario => {
            const id_usuario = resUsuario.data.id_usuario; // Obtener el id_usuario de la respuesta
            console.log(this.newAlumno); // Imprimir en la consola
            axios.put(this.postURL + '/alumno', { ...this.newAlumno, id_usuario }, config_request)
              .then(resAlumno => {
                console.log(resAlumno.data);
              })
              .catch(errorAlumno => {
                console.log(errorAlumno);
              });
          })
          .catch(errorUsuario => {
            console.log(errorUsuario);
          });

        //this.newAlumno = {};
        this.newUsuario = {};
      }      
    }
  };
  </script>
  
  <style>
  .modal {
    display: none;
    background-color: rgba(0, 0, 0, 0.5);
    position: fixed;
    top: 0;
    right: 0;
    bottom: 0;
    left: 0;
    z-index: 1050;
    overflow: hidden;
    outline: 0;
    transition: opacity 0.15s;
  }
  
  .modal.show {
    display: block;
  }
  
  .modal-dialog {
    max-width: 500px;
    margin: 1.75rem auto;
  }
  
  .modal-content {
    background-color: #fff;
    border: 1px solid rgba(0, 0, 0, 0.2);
    border-radius: 0.3rem;
    box-shadow: 0 0.25rem 0.5rem rgba(0, 0, 0, 0.5);
  }
  
  .modal-header {
    padding: 0.75rem;
    border-bottom: 1px solid #dee2e6;
  }
  
  .modal-body {
    position: relative;
    padding: 1rem;
  }
  
  .modal-footer {
    padding: 0.75rem;
    border-top: 1px solid #dee2e6;
  }
  </style>
  