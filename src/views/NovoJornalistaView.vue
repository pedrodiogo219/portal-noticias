<template>
    <h1>Novo Jornalista</h1>
    <form @submit.prevent="submit" class="form-container">
        <div class="form-field">
            <label for="nome">Nome*</label>
            <input id="nome" type="text" v-model="nome"/>
        </div>
        <div class="form-field">
            <label for="cpf">CPF*</label>
            <input id="cpf" type="text" v-model="cpf"/>
        </div>
        <div class="form-field">
            <label for="telefone">Telefone</label>
            <input id="telefone" type="text" v-model="telefone"/>
        </div>

        
        <input type="submit" value="Cadastrar jornalista"/>
    </form>


</template>

<script>
import router from '@/router';
import axios from 'axios';

export default {
    name: "NovoJornalistaView",
    data() {
        return {
            nome: '',
            cpf: '',
            telefone: ''
        }
    },

    methods: {
        async submit(){
            if (this.nome.trim() === ''){
                alert('Formulário inválido: Nome não pode ser vazio');
                return;
            }

            if(this.cpf.trim() === ''){
                alert('Formulário inválido: CPF não pode ser vazio');
                return;
            }

            const novoJornalista = {
                nome: this.nome,
                cpf: this.cpf,
                telefone: this.telefone
            }

            await axios.post("http://localhost:8080/api/jornalista", novoJornalista)
                .then(()=>{
                    alert('Jornalista cadastrado com sucesso');
                    router.push('/nova-noticia');
                })
                .catch(function (error) {
                    let error_msg = '[Erro] ' + error.message
                    if (error.response) {
                        // The request was made and the server responded with a status code
                        // that falls out of the range of 2xx
                        console.log(error.response.data);
                        console.log(error.response.status);
                        console.log(error.response.headers);
                        error_msg += '\n' + error.response.data.message;
                    } else if (error.request) {
                        // The request was made but no response was received
                        // `error.request` is an instance of XMLHttpRequest in the browser and an instance of
                        // http.ClientRequest in node.js
                        console.log(error.request);
                    } else {
                        // Something happened in setting up the request that triggered an Error
                        console.log('Error', error.message);
                    }

                    console.log(error.config);
                    alert(error_msg);
                }) 

        }
    }
}

</script>

<style scoped>

input{
    font-family: 'Times New Roman', Times, serif;
    border: 1px solid black;
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
