<template>
    <h1>feed</h1>
    <button v-on:click="mostra()">mostra</button>

    <div id="listaNoticias">
        <ResumoNoticia v-for="(noticia, index) in this.$parent.noticias.value" :key="index" :noticia="noticia"></ResumoNoticia>
    </div>

</template>

<script>
    import ResumoNoticia from './ResumoNoticia.vue';


    export default {
    created() {
        console.log(this.$parent.noticias);
    },
    methods: {
        mostra: function () {
            console.log(this.$parent.noticias);
        }
    },
    components: { ResumoNoticia }
}
</script>


<style scoped>

#listaNoticias{
    display: flex;
    flex-direction: row;
    flex-wrap: wrap;
}

</style>