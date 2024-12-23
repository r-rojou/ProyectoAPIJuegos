<script>
import { RouterLink, RouterView } from 'vue-router'
import Componente1 from './components/Componente1.vue';
export default{
  components:{
    Componente1
  },
  data(){
    return{
      arregloOpiniones: [],
      arregloJuegosGlobal: [],
      arregloLikesGlobal: [],
      apiConsumida: false,
      usuariosPermitidos:{
        nombre: 'nombre',
        apellido: 'apellido'
      },
      flagAutenticacion: false,
    }
  },
  methods:{
    llenarArregloOpiniones(){
      console.log('Funciona llenarArregloOpiniones');
      this.arregloOpiniones.push([]);
      this.arregloLikesGlobal.push(false);
    },
    notificarApiConsumida(unArreglo){
      console.log('La API fue consumida exitosamente');

      this.apiConsumida = true;
      this.arregloJuegosGlobal = unArreglo;
    },
    agregarOpinion(objOpinion){
      console.log('Funciona agregarOpinion');
      console.log(objOpinion);
      this.arregloOpiniones[objOpinion.idJuego].push(objOpinion);
    },
    eliminarOpinion(objIndices){
      let elementoEliminado = this.arregloOpiniones[objIndices.indiceJuego].splice(objIndices.indiceOpinion,1);
      console.log(elementoEliminado);
      alert(`La opinión ${objIndices.indiceOpinion} del juego ${objIndices.indiceJuego} fue eliminada =>: ${elementoEliminado[0].nombre} - ${elementoEliminado[0].opinion}`);
    },
    editarOpinion(objNuevaOpinion){
      console.log('Opinion para editar');
      console.log(objNuevaOpinion);

      this.arregloOpiniones[objNuevaOpinion.indiceJuego][objNuevaOpinion.indiceOpinion] = objNuevaOpinion.objNuevaOpinion;
      alert(`La nueva opinión es =>: ${objNuevaOpinion.nuevaOpinion.nombre} - ${objNuevaOpinion.nuevaOpinion.opinion}`);
    },
    verificarAutenticacion(objAutenticacion){
      if(this.usuariosPermitidos.nombre == objAutenticacion.nombre && this.usuariosPermitidos.apellido == objAutenticacion.apellido){
        this.flagAutenticacion = true;
      }
      else{
        this.flagAutenticacion = false;
      }

    },
    registrarLike(elIndice){
      console.log('Se ha registrado un like con indice: ', elIndice);
      let valorLike = !this.arregloLikesGlobal[elIndice];
      this.arregloLikesGlobal[elIndice] = valorLike;
    },
    cantidadArregloOpiniones(){
      console.log(this.arregloOpiniones.length);
      console.log(this.arregloOpiniones);
    },
    cantidadArregloLikes(){
      console.log(this.arregloLikesGlobal.length);
      console.log(this.arregloLikesGlobal);
    }

  }
}
</script>

<template>
  <header>
    <div class="container-fluid" id="divNav">
      <div class="row">
        <div class="col-3">
          <figure class="contenedorImagen">
            <img alt="logo" class="logo" src="..\src\assets\logo.png"/>
          </figure>
        </div>
        <div class="col-6">
          <h1>- Bienvenido a Reviews JoePino.com -</h1>
          <hr>
        </div>
        <div class="col-3">
          <nav>
            <RouterLink to="/" class="color">Home</RouterLink> |
            <RouterLink to="/about" class="color">About</RouterLink> |
            <RouterLink to="/juegos" class="color">Juegos</RouterLink> |
            <RouterLink to="/autenticacion" class="color">Autenticar</RouterLink> |
            <RouterLink to="/administracion" class="color">Cuenta</RouterLink> |
          </nav>
        </div>
      </div>
    </div>



    <div>
      <Componente1 msg="Mensaje enviado desde App.vue a Componente1" />


    </div>
  </header>
  <br><br><br>

  <div id="divRouterView">
    <p>RouterView.</p>
    <RouterView v-slot="{Component}"
        v-on:llenar-arreglo-opiniones="llenarArregloOpiniones"
        v-on:api-consumida="notificarApiConsumida"
        v-on:agregar-opinion="agregarOpinion"
        v-on:eliminar-opinion="eliminarOpinion"
        v-on:editar-opinion="editarOpinion" 
        v-on:datos-autenticacion="verificarAutenticacion" 
        v-on:like-enviado="registrarLike" 
        v-bind:arregloOpinionJuego ="arregloOpiniones"
        v-bind:arregloLleno = "apiConsumida" 
        v-bind:arregloJuegosRecibido = "arregloJuegosGlobal" 
        v-bind:estaRegistradoAutenticacion = "flagAutenticacion" 
        v-bind:estaRegistradoJuegos = "flagAutenticacion" 
        v-bind:estaRegistradoAdministracion = "flagAutenticacion" 
        v-bind:arregloJuegos ="arregloJuegosGlobal" 
        v-bind:arregloLikes = "arregloLikesGlobal"
        >
        
        <transition name="router-anim">  
          <component :is="Component" />  
        </transition>
    </RouterView>
  </div>
  <hr>
  <div id="botonCantidad">
    <button class="btn btn-md btn-dark" v-on:click="cantidadArregloOpiniones">Ver cantidad de opiniones</button>
    <button class="btn btn-md btn-dark" v-on:click="cantidadArregloLikes">Ver cantidad de likes</button>
  </div> <br><br>


</template>

<style scoped>
  #divRouterView{
    background-color: rgb(33, 13, 70);
    text-align: center;
    margin: 2%;
    border: solid;
    border-radius: 10px;
    color: white;
  }
  #divNav{
    background-color:rgb(33, 13, 70);
    position: fixed;
    top: 0;
    padding: 1rem;
    z-index: 1000;
  }
  h1{
    text-align: center;
    color: white;
    margin: 2%;

  }
  hr{
    color: white;
  }
  nav{
    text-align:end;
    margin: 2%;
    font-size: larger;
  }

  nav .color{
    color: white;
  }

  nav .color:hover{
    color: blue;
  }
  .contenedorImagen{
    max-width: auto;

  }
  .logo{
    width: 25%;
    margin: 3%;
    padding: 3%;
    border: solid;
    border-style: dotted;
    border-color: white;
    border-radius: 100px;
  }

  .router-anim-enter-active{
    animation: coming 1s;
    animation-delay: 1s;
    opacity: 0;
  }

  .router-anim-leave-active{
    animation: going 1s;
  
  }
  #botonCantidad{
    display: flex;
    justify-content: space-evenly;
  }
  

  @keyframes coming{
    from{
      transform: translateX(-50px);
      opacity: 0;
    }
    to{
      transform: translateX(0);
      opacity: 1;
    }
    
  }

  @keyframes going{
    0%{
      transform: translateX(0);

    }
    100%{
      transform: translateX(-50px);
      opacity: 0;
    }
  }

</style>
