<template>
    <h1>Nova notícia</h1>
    <form @submit.prevent="submit" class="form-container">
        <div class="form-field">
            <label for="titulo">Titulo</label>
            <input id="titulo" type="text" placeholder="Ex: O Circo está na cidade!" v-model="titulo"/>
            <!-- {{ titulo }} -->
        </div>

        <div class="form-field">
            <label for="descricao">Descricao</label>
            <textarea v-model="descricao"></textarea>
            <!-- {{ descricao }} -->
        </div>

        <div class="form-field">
            <label for="corpo">Corpo</label>
            <textarea v-model="corpo"></textarea>
            <!-- {{ corpo }} -->
        </div>

        <div class="form-field">
            <label for="imagem">Imagem</label>
            <input v-model="imagem" placeholder="link da imagem"/>
            <!-- {{ imagem }} -->
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
            corpo: '',
            imagem: ''
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
                corpo: this.corpo,
                imagem: this.imagem
            });

            localStorage.setItem("noticias", JSON.stringify(this.noticias));

            router.push('/noticia/' + newId);
        }
    }
}
</script>

<style scoped>

input{
    font-family: 'Times New Roman', Times, serif;
    border: 1px solid black;
}
textarea{
    font-family: 'Times New Roman', Times, serif;
}

.form-field{
    font-size: 16px;
    padding: 10px 20px;
    justify-content: space-between;
    display: flex;
    width: 90%;
    margin: auto;
}

.form-field input{
    width: 65%;
    font-size: 16px;
}

.form-field textarea{
    width: 65%;
    font-size: 16px;
}

label {
    padding-right: 10px;
}
</style>