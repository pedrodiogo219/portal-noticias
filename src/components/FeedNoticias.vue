<template>
    <h1>feed</h1>
    <button v-on:click="mostra()">mostra</button>

    <ul>
        <li v-for="(noticia, index) in this.$parent.noticias.value" :key="index">{{noticia.titulo}}</li>
    </ul>

</template>

<script>
    export default {
        created(){
            console.log(this.$parent.noticias)
        },
        methods: {
            mostra: function(){
                console.log(this.$parent.noticias)
            }
        }
    }
</script>