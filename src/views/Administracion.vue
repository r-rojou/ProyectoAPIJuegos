<script>
export default{
    props:{
        estaRegistradoAdministracion:{
            type:Boolean,
            required:true
        },
        arregloLikes:{
            type:Array,
            required: true
        },
        arregloJuegos:{
            type:Array,
            required: true
        }
    },
    data(){
        return{
            titulo:'Este es el componente Administracion.vue',
            arregloNombreJuegos:[],
            cantidadCoins: 0,
            claseCoins: '',
            claseColorBarra: '',
        }
    },
    methods:{
        incrementarCoins(){
            if(this.cantidadCoins<100){
                this.cantidadCoins = (this.cantidadCoins + 2);
                console.log(this.cantidadCoins);
                this.claseCoins = `width: ${this.cantidadCoins}%`;
                console.log(this.claseCoins);
                if(this.cantidadCoins<=20){
                    this.claseColorBarra = 'progress-bar bg-success';
                }
                else if(this.cantidadCoins>20 && this.cantidadCoins<=30){
                    this.claseColorBarra = 'progress-bar bg-warning';
                }
                else{
                    this.claseColorBarra = 'progress-bar bg-danger';
                }
            }
        }

    },
    computed:{
        cantidadLikes(){
            let losLikes=0;
            for(let i=0; i<this.arregloLikes.length; i++){
                if(this.arregloLikes[i]==true){
                        losLikes=losLikes+1;
                        this.arregloNombreJuegos.push(this.arregloJuegos[i].name);
                }// fin if
            }// fin for
            return losLikes;
        }// fin cantidadLikes
    }
}
</script>
<template>
    <div id="divAdministracion">
        <h1 v-html="titulo"></h1>
        <div v-if="estaRegistradoAdministracion">
            <div class="container">
                <h1 class="registrado">Bienvenido</h1>
            </div>
 
            <h1>Usted ha dado esta cantidad de likes: {{ cantidadLikes }}</h1>
            <ul>
                <li v-for="nombre in arregloNombreJuegos">Le diste me gusta al juego: {{ nombre }} </li>
            </ul>
            
            <div id="divCompraCoins">
                <p>¿Deseas comprar Coins para los juegos?</p>
                <button class="btn btn-secondary" v-on:click="incrementarCoins">Agregar Coins</button>
                <br> <br>               

                <!--Progress Bar-->
                <div class="progress" role="progressbar" aria-label="Basic example" v-bind:aria-valuenow="cantidadCoins" aria-valuemin="0" aria-valuemax="100">
                     <div v-bind:class="claseColorBarra" v-bind:style="claseCoins"></div>
                </div> <br>
                <!--fin Progress Bar-->
            </div>
        </div>
        <div v-else>
            <h1 class="noRegistrado">USTED NO ESTA REGISTRADO</h1>
        </div>
    </div>
</template>

<style scoped>
.registrado{
    color: white;
    background-color: rgb(33, 13, 70);
    margin: 2%;
}
.noRegistrado{
    color: white;
    background-color: red;
}
#divAdministracion{
    background-color: lightgray;
    color:black;
}
#divCompraCoins{
    margin: 2%;

}
</style>