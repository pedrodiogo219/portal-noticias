<template>
    <div id="container">
        <h3>{{ noticia.titulo }}</h3>
        <p>{{ noticia.descricao }}</p>
    </div>
</template>

<script>

export default {
    props: ['noticia']
}
</script>

<style scoped>
#container{
    border: 1px solid black;
    display: block;
}
</style>