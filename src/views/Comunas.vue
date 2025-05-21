<template>
  <div class="container">
    <h1 class="text-start">Listado Comunas</h1>
    <button @click="newComuna()"
            class="btn btn-success mx-2">
      <font-awesome-icon icon="plus" />
    </button>
    <table class="table">
      <thead>
        <tr>
          <th scope="col">#</th>
          <th scope="col">Code</th>
          <th scope="col">Name</th>
          <th scope="col">Municipality</th>
          <th scope="col">Actions</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(comuna,index) in comunas" :key="index">
          <th scope="row">{{index+1}}</th>
          <td>{{comuna.comu_codi}}</td>
          <td>{{comuna.comu_nomb}}</td>
          <td>{{comuna.muni_nomb}}</td>
          <td>
            <button @click="deleteComuna(comuna.comu_codi)"
                    class="btn btn-danger mx-2">
              <font-awesome-icon icon="trash" />
            </button>
            <button @click="editComuna(comuna.comu_codi)"
                    class="btn btn-warning mx-2">
              <font-awesome-icon icon="pencil" />
            </button>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>
<script>
import axios from 'axios'

export default {
  name: 'Comuna',
  data() {
    return {
      comunas: []
    }
  },
  mounted() {
    axios
      .get('http://127.0.0.1:8000/api/comunas')
      .then(response => {
        // Aquí asignamos el arreglo comunas desde la respuesta
        this.comunas = response.data.comunas || []; 
        // En caso de que no exista la propiedad, asignamos un arreglo vacío
      })
      .catch(error => {
        console.error('Error al obtener comunas:', error);
        // Puedes también mostrar un mensaje en pantalla si quieres
      })
  }
}
</script>
