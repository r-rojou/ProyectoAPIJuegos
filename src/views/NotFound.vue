<script>
export default{
    data(){
        return{
            notFound: 'ERROR 404 - NOT FOUND'
        }
    },
    methods:{

    }
}
</script>

<template>
    <div id="divNotFound">
        <h1 v-html="notFound"></h1>
    </div>

</template>

<style scoped>
    #divNotFound{
        background-color: red;
        color: white;
    }
</style>