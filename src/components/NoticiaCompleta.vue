<template>
  <div v-if="this.noticia != undefined">
    <h1>{{ this.noticia.titulo }}</h1>
    <strong> {{ this.noticia.descricao }}</strong>
    <p>{{ this.noticia.corpo }}</p>
  </div>
  <div v-else>
    <NotFound></NotFound>
  </div>

</template>
<script>
import NotFound from './NotFound.vue';
  export default {
    created() {
        this.noticias = JSON.parse(localStorage.getItem("noticias")) || [];
        console.log(this.noticias);
        console.log(this.$route.params.id);
        this.noticia = this.noticias.find(n => n.id === Number(this.$route.params.id));
        console.log(this.noticia);
    },
    components: { NotFound }
};
</script>