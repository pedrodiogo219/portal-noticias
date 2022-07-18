<template>
  <div v-if="this.noticia != undefined">
    <h1>{{ this.noticia.titulo }}</h1>
    <div>
      <img v-bind:src="this.noticia.imagem">
    </div>
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
        this.noticia = this.noticias.find(n => n.id === Number(this.$route.params.id));
    },
    components: { NotFound }
};
</script>