<template> <!--Template para insersión de datos-->
  <div>
    <form v-on:submit.prevent="guardar">
      <div class="form-row">
        <div class="col-md-4 mb-3">
          <label>Dpi: </label>
          <input type="text" class="form-control" id="Dpi" placeholder="Dpi" v-model="dpi" required>
        </div>
        <div class="col-md-4 mb-3">
          <label>Nit:</label>
          <input type="text" class="form-control" id="Nit" placeholder="Nit" v-model="nit" required>
        </div>
        <div class="col-md-4 mb-3">
          <label>Nombre:</label>
          <input type="text" class="form-control" id="Nombre" placeholder="Nombre" v-model="nombre" required>
        </div>
        <div class="col-md-4 mb-3">
          <label >Apellido:</label>
          <input type="text" class="form-control" id="Apellido" placeholder="Apellido" v-model="apellido" required>
        </div>
        <div class="col-md-4 mb-3">
          <label>Direccion:</label>
          <input type="text" class="form-control" id="Direccion" placeholder="Direccion" v-model="direccion" required>
        </div>
        <div class="col-md-4 mb-3">
          <label>Municipio:</label>
          <input type="text" class="form-control" id="Municipio" placeholder="Municipio" v-model="municipio" required>
        </div>
      </div>
      <button class="btn btn-primary" type="submit">Enviar</button>
    </form>
  </div>
</template>

<template> <!--Template para obtener datos generales del registro-->
  <div>
        <table class="table">
            <thead>
                <tr>
                    <th scope="col">#</th>
                    <th scope="col">Dpi</th>
                    <th scope="col">Nit</th>
                    <th scope="col">Nombre</th>
                    <th scope="col">Apellido</th>
                    <th scope="col">Direccion</th>
                    <th scope="col">Municipio</th>
                </tr>
            </thead>
            <tbody>
                <tr v-for="persona in listaRegistros" :key="persona.id" v-on:click="editar(persona.id)">
                    <th scope="row">{{ persona.id }} </th>
                    <td>{{ persona.dpi }}</td>
                    <td>{{ persona.nit }}</td>
                    <td>{{ persona.nombre }}</td>
                    <td>{{ persona.apellido }}</td>
                    <td>{{ persona.direccion }}</td>
                    <td>{{ persona.municipio_id }}</td>
                </tr>
            </tbody>
          </table>
    </div>
</template>


<script>
  import axios from 'axios';

  export default {
    name: 'AppView',
    data(){ //Almacenamiento para Get de Registros Generales 
      return{
        listaRegistros:null
      }
    },
    components: {
   
    },
    
    /*data: function(){ //Request para Post de Registro
      return{
        dpi: "",
        nit: "",
        nombre: "",
        apellido: "",
        direccion: "",
        municipio: "",
      }
    },*/
    methods:{
     /* guardar(){  //Metodo Para Guardar los registros generales
        let json = {
          "dpi": this.dpi,
          "nit": this.nit,
          "nombre": this.nombre,
          "apellido": this.apellido,
          "direccion": this.direccion,
          "municipio_id": this.municipio
        };
        axios.post('https://servicios.mem.gob.gt/api/api_prueba/prueba/insert', json)
        .then(data => {
          console.log(data);
          this.$router.push('registro');
        })
      },*/

     editar(id){
      console.log(id);
      axios.put('https://servicios.mem.gob.gt/api/api_prueba/prueba/update')
     }

     /*eliminar(id){
      axios.delete('https://servicios.mem.gob.gt/api/api_prueba/prueba/delete')
     }*/
      
    },
    mounted:function(){ //Metodo para obtener los registros generales
        axios.get('https://servicios.mem.gob.gt/api/api_prueba/prueba/read')
        .then(data => {
          this.listaRegistros = data.data;
        })
    }


  }
</script>