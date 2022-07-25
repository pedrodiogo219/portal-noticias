<template>
  <div v-if="this.noticia != undefined">
    <h1>{{ this.noticia.titulo }}</h1>
    <div>
      <img v-bind:src="this.noticia.imagem">
    </div>
    <strong><h4>{{ this.noticia.descricao }}</h4></strong>
    <span>Escrito por: {{ this.jornalista.nome }}</span>
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

        if(this.noticia){
          this.jornalistas = JSON.parse(localStorage.getItem("jornalistas")) || [];
          this.jornalista = this.jornalistas.find(j => j.id === this.noticia.idJornalista)
        }

        
    },
    components: { NotFound }
};
</script>

<style scoped>

img{
  max-width: 80%;
  max-height: 100%;
}

p{
  text-align: justify;
  padding: 0 20px;
}

</style>