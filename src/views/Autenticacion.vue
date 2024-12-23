<script>    
export default{
    props:{
        estaRegistradoAutenticacion:{
            type: Boolean,
            required: true,
        }
    },
    data(){
        return{
            titulo: 'Este es el componente Autenticacion.vue (Ingreso Nombre: nombre // Apellido: apellido)',
            form:{
                nombre: '',
                apellido: '',
            },
            mensaje: '',
        }
    },
    methods:{
        atraparDatosAutenticacion(){
            console.log('Emitimos datos de autenticacion al padre')
            alert('Vamos a enviar los datos al padre')
            let elNombre = this.form.nombre;
            let elApellido = this.form.apellido;
            let objTempAutenticacion ={
                nombre: elNombre,
                apellido: elApellido
            }

            this.$emit('datos-autenticacion', objTempAutenticacion);
            this.form.nombre = '';
            this.form.apellido = '';

        }

    },
    computed:{
        estaAutenticado(){
            if(this.estaRegistradoAutenticacion){
                return 'El usuario está autenticado'
            }
            else{
                  return 'El usuario NO está autenticado'
            }
          
        }
    }
}
</script>


<template>
    <div id="divAutenticacion">
        <h3 v-html="titulo"></h3>
        <br> <hr>
        <h2> {{ estaAutenticado }}</h2>
        <hr> 
        <div class="container">
            <form>
            <div class="mb-3">
              <label for="txtNombre" class="form-label">Nombre: </label>
              <input type="text" class="form-control" id="txtNombre" v-model="form.nombre">
            </div>
            <div class="mb-3">
              <label for="txtApellido" class="form-label">Apellido: </label>
              <input type="text" class="form-control" id="txtApellido" v-model="form.apellido">
            </div> <br>

            <button type="button" class="btn btn-lg" @click="atraparDatosAutenticacion">Ingresar</button> <br> <br>
        </form>
        </div>
        

    </div>
</template>

<style scoped>
    #divAutenticacion{
        background-color: lightgray;
        color: black;
        margin: 2%;
        border-radius: 50px;
    }

    h2{
        color: rgb(255, 255, 255);
        background-color: rgb(109, 19, 109);
    }

    .btn{
        background-color: purple;
        color: white;
    }
</style>