<template>
    <h1>Nova notícia</h1>
    <form @submit.prevent="submit" class="form-container">
        <div class="form-field">
            <label for="titulo">Titulo*</label>
            <input id="titulo" type="text" placeholder="Ex: O Circo está na cidade!" v-model="titulo"/>
            <!-- {{ titulo }} -->
        </div>

        <div class="form-field">
            <label for="descricao">Descricao*</label>
            <textarea v-model="descricao"></textarea>
            <!-- {{ descricao }} -->
        </div>

        <div class="form-field">
            <label for="corpo">Corpo*</label>
            <textarea v-model="corpo"></textarea>
            <!-- {{ corpo }} -->
        </div>

        <div class="form-field">
            <label for="imagem">Imagem*</label>
            <input v-model="imagem" placeholder="link da imagem"/>
            <!-- {{ imagem }} -->
        </div>

        <div class="form-field">
            <label for="jornalista">Jornalista*</label>
            <select v-model="idJornalista">
                <option disabled value=0>Selecione o jornalista</option>
                <option v-for="option in options" :key="option.id" :value="option.id">
                    {{ option.nome }}
                </option> 
            </select>
        </div>

        <input type="submit" value="Enviar notícia"/>
    </form>

    <div class="link">
        Seu jornalista não está cadastrado?
        <a href="/novo-jornalista">Cadastre um jornalista</a>
    </div>
</template>

<script>
import router from '@/router';
import axios from 'axios';

export default {
    name: "NovaNoticiaView",
    async created() {
        const response = await axios.get("http://localhost:8080/api/jornalista");
        this.options = response.data;
    },
    data() {
        return {
            titulo: '',
            descricao: '',
            corpo: '',
            imagem: '',
            idJornalista: 0,

            options: this.options
            // options: JSON.parse(localStorage.getItem('jornalistas')) || []
        }
    },

    methods: {
        submit(){
            if (this.titulo.trim() === '' || this.descricao.trim() === '' || this.corpo.trim() === '' || this.idJornalista === 0){
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
                imagem: this.imagem,
                idJornalista: this.idJornalista
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

.form-field select{
    width: 65%;
    font-size: 16px;
}

label {
    padding-right: 10px;
}

.link{
    padding-top: 20px;
}
</style>