<template>
    <h1>feed</h1>

    <div id="listaNoticias" v-if="noticiasExists()">
        <ResumoNoticia v-for="(noticia, index) in this.$parent.noticias.value" :key="index" :noticia="noticia"></ResumoNoticia>
    </div>
    <div v-else>
        <p>Nenhuma notícia disponivel</p>
    </div>

</template>

<script>
    import ResumoNoticia from './ResumoNoticia.vue';

    export default {
    data() {
        return {
            noticiasExists: () => {
                return (JSON.stringify(this.$parent.noticias.value) != '[]')
            }
        }
    },
    components: { ResumoNoticia }
}
</script>


<style scoped>

#listaNoticias{
    display: flex;
    flex-direction: column;
    flex-wrap: wrap;
}

</style>