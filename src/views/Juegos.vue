<script>
export default{
    props:{
        arregloLleno:{
            type: Boolean,
            required: true
        },
        arregloJuegosRecibido:{
            type:Array,
            required: true
        },
        estaRegistradoJuegos:{
            type: Boolean,
            required: true,
        }
    },
    data(){
        return{
            titulo: 'Este es el componente Juegos.vue',
            arregloJuegos: []
        }
    },
    methods:{
        enviarOpinion(nombreJuego, unIndice){
            console.log('Nombre juego recibido: ', nombreJuego);
            console.log('indice: ', unIndice);
            let nombreCompuesto = `${unIndice}-${nombreJuego}`;
            this.$router.push(`/opinion/${nombreCompuesto}`);

        },
        enviarLike(unIndice){
            this.$emit('like-enviado', unIndice);
        }

    },
    created(){
        if(this.arregloLleno == false){

        
            let url = 'https://api.rawg.io/api/games?key=548ac8fcc5ad4b3780b81ed0b0a992c6&platforms=1';
            fetch(url)
            .then((respuesta)=>{
                respuesta.json()
                .then((objRespuesta)=>{
                    console.log(objRespuesta);
                    // Los juegos se encuentra en la propiedad results
                    for(let juego of objRespuesta.results){
                        this.arregloJuegos.push(juego);
                        this.$emit('llenar-arreglo-opiniones');
                    }
                    console.log('Recorrido de respuesta terminado');
                    console.log(this.arregloJuegos);
                    this.$emit('api-consumida', this.arregloJuegos);

                })
                .catch((errorTransformacion)=>{
                    console.log('Error transformando a json: ', errorTransformacion)
                });

            })
            .catch((error)=>{
                console.log('Error consumiendo la API: ', error)
            })
        }
    }
}
</script>

<template>
    <div id="divJuegos">
        <h2 v-html="titulo"></h2>
        <div class="contenedorFlex">
            <div class="contenidoFlex" v-for="(unJuego, index) in arregloJuegosRecibido" v-bind:key="index">
                <p v-html="unJuego.name"></p>
                <figure class="contenedorImagen">
                    <img class="contenidoImagen" v-bind:src="unJuego.background_image">
                </figure>
                <p>Rating: <span v-html="unJuego.rating"></span></p>
                <p>Released: <span v-html="unJuego.released"></span></p>
                <div id="divBotones">
                    <button class="btnOpinar btn btn-lg btn-light" v-on:click="enviarOpinion(unJuego.name, index)">Opinar</button>
                    <button v-if="estaRegistradoJuegos" class="btnOpinar btn btn-danger" v-on:click="enviarLike(index)">Like</button>
                </div>  
                
                <br>
                <br>

            </div>

        </div>

    </div>
</template>

<style scoped>
    #divJuegos{
        background-color: rgba(83, 49, 209, 0.438);
        margin: 2%;
        border-style: groove;

    }
    .contenedorFlex{
        display: flex;
        flex-wrap: wrap;
        margin: 2%;
        background-color: rgba(76, 45, 187, 0);

    }
    .contenidoFlex{
        background-color: black;
        width: 300px;
        margin: 3%;
        border-style: groove;
        border: solid;

    }

    .contenedorImagen{
        max-width: auto;

    }

    .contenidoImagen{
        width: 100%;
    }
    #divBotones{
        display: flex;
        justify-content: space-evenly;
    }
</style>