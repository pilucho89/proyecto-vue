
<template>
<div class="container">
<div class="row">
      <form @submit.prevent="agregarUsuario">
      <div class="col m12 card-panel">
        <div class="col m4">
          <label>Nombre</label>
          <input type="text" v-model="nombre">
        </div>
        <div class="col m4">
          <label>Apellido</label>
          <input type="text" v-model="apellido">
        </div>
      </div>
        <div class="row">
          <div class="col m4">
          <label>Edad</label>
          <input type="number" v-model="edad">
          </div>
        <div class="col m4">
          <label>Estado Civil</label>
              
                <select v-model="estado_civil">
                  <option value="">Seleccione</option>
                  <option v-for="estado in estados_civiles" v-bind:key="estado" v-bind:value="estado.descripcion">{{estado.descripcion}}</option>

              </select>
              
              
      </div>
      <div class="col m4">
          <label>Correo</label>
              <input type="email" v-model="correo">
      </div>
    </div>
    <div class="row">
        <form @submit.prevent="agregarPasatiempo">
        <div class="col m4 card-panel">
          <label>Pasatiempo</label>
          <input type="text" v-model="pasatiempo">
          <button type="submit" class="btn indigo darken-3">Agregar Pasatiempos<i class="material-icons rigth">send</i></button>
          <hr>
          <ul>
            <li v-for="(pasatiempo, index) in pasatiempos" v-bind:key="pasatiempo">{{pasatiempo.id}}-{{pasatiempo.descripcion}} <a href="#!" @click="pasatiempos.splice(index,1)"><i class="material-icons">close</i></a></li>
          </ul>
      </div>
    </form>
      <div class="col m4">
        <label><input type="checkbox" v-model="suscrito"> <span>Suscribirse al boletin de noticias</span></label>
      
    </div>
    <div class="row">
      <button type="submit" class="btn indigo darker 4">Agregar Usuario <i class="material-icons rigth">add_circle</i></button>
    </div>
    

</div>
</form>
</div>
<div class="row">
  <div class="col m12">
    <table class="table bordered striped">
      <thead>
        <tr>
          <th>Name</th>
          <th>Apellido</th>
          <th>Edad</th>
          <th>Estado Civil</th>
          <th>Correo</th>
          <th>Pasatiempos</th>
          <th>Suscrito</th>
          <th>Editar</th>
          <th>Eliminar</th>
        </tr>
      </thead>
      <tbody>
        
          <tr v-for="(usuario, index) in usuarios" v-bind:key="usuario">
            <td>{{usuario.nombre}}</td>
            <td>{{usuario.apellido}}</td>
            <td>{{usuario.edad}}</td>
            <td>{{usuario.estado_civil}}</td>
            <td>{{usuario.correo}}</td>
            <td>
              <ul>
                <li v-for="pasatiempo in usuario.pasatiempos" v-bind:key="pasatiempo">{{pasatiempo.id}}-{{pasatiempo.descripcion}}</li>
              </ul>
            </td>
            <td><label><input type="checkbox" disabled v-model="usuario.suscrito"><span></span></label></td>
            <td><a href="#!"><i class="material-icons">create</i></a></td>
            <td><a href="#!" @click="eliminar(index)"><i class="material-icons">delete</i></a></td>




          </tr>
        
      </tbody>
    </table>
  </div>
</div>
</div>


</template>

<script>
/*document.addEventListener('DOMContentLoaded',function(){
  var elems=document.querySelectorAll('select');
  var instances=M.FormSelect.init(elems, options);
});*/
import M from 'materialize-css'
export default {
  name: 'App',
  data(){
     return{
      nombre: '',
      apellido: '',
      edad: 0,
      estado_civil:'',
      correo:'',
      suscrito: false,
      pasatiempo: '',
      pasatiempos: [],
      select_instances:[],
      usuarios: [],
      estados_civiles: [
        {
          id: 'S',
          descripcion:'NO SE'
        },
        {
          id: 'C',
          descripcion:'Casado'
        },
        {
          id: 'D',
          descripcion:'Divorciado'
        },
        {
          id: 'V',
          descripcion:'Viudo'
        }
      ]
    }
    
  },
  mounted()
  {
    var elems=document.querySelectorAll('select');
     this.select_instances=M.FormSelect.init(elems, null);
  },
  methods:{
       cleanForm(){
    this.nombre='';
      this.apellido= '';
      this.edad= 0;
      this.estado_civil='';
      this.correo='';
      this.suscrito= false;
      this.pasatiempo ='';
      this.pasatiempos= [];
      this.select_instances=[];
  },
    agregarUsuario()
    {


      var data={
        nombre:this.nombre,
        edad:this.edad,
        apellido:this.apellido,
        correo:this.correo,
        estado_civil:this.estado_civil,
        suscrito:this.suscrito,
        pasatiempos:this.pasatiempos
        
      };
      this.usuarios.push(data);
      this.cleanForm();
    },

    agregarPasatiempo()
  {
    if(this.pasatiempo !== null && this.pasatiempo !== ""){
      console.log("Pasatiempo Not Found")
    var total=this.pasatiempos.length;
    var ultimo=0;
    if(total>0)
    {
      ultimo=this.pasatiempos[total-1].id;
    }
    var data={
      id: ultimo+1,
      descripcion: this.pasatiempo
    };
    this.pasatiempos.push(data);
    this.pasatiempo='';
  }
    }
  ,
  eliminar(index){
    if (!confirm('¿Desea eliminar el registro?')) return;
    this.usuarios.splice(index,1);
  },

    
  }
  

}
</script>


