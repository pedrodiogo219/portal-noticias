<template>
    <h1>nova noticia</h1>
    <form @submit.prevent="submit">
        <div>
            <label for="titulo">Titulo</label>
            <input id="titulo" type="text" placeholder="Ex: O Circo está na cidade!" v-model="titulo"/>
            <!-- {{ titulo }} -->
        </div>

        <div>
            <label for="descricao">Descricao</label>
            <textarea v-model="descricao"></textarea>
            <!-- {{ descricao }} -->
        </div>

        <div>
            <label for="corpo">Corpo</label>
            <textarea v-model="corpo"></textarea>
            <!-- {{ corpo }} -->
        </div>


        <input type="submit" value="Enviar notícia"/>
    </form>
</template>

<script>
import router from '@/router';

export default {
    name: "NovaNoticiaView",
    data() {
        return {
            titulo: '',
            descricao: '',
            corpo: ''
        }
    },

    methods: {
        submit(){
            if (this.titulo.trim() === '' || this.descricao.trim() === '' || this.corpo.trim() === ''){
                alert('Formulário inválido: Nenhum campo pode ficar vazio.');
                return
            }

            this.noticias = JSON.parse(localStorage.getItem('noticias')) || [];
    
            let newId = 1;

            if (this.noticias.length !== 0){
                newId = Math.max(...this.noticias.map(n => n.id)) + 1;
            }


            this.noticias.push({
                id: newId,
                titulo: this.titulo,
                descricao: this.descricao,
                corpo: this.corpo
            });

            localStorage.setItem("noticias", JSON.stringify(this.noticias));

            router.push('/noticia/' + newId);
        }
    }
}
</script>