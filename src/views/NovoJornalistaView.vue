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
        submit(){
            if (this.nome.trim() === ''){
                alert('Formulário inválido: Nome não pode ser vazio');
                return;
            }

            if(this.cpf.trim() === ''){
                alert('Formulário inválido: CPF não pode ser vazio');
                return;
            }

            this.jornalistas = JSON.parse(localStorage.getItem('jornalistas')) || [];

            let newId = 1;

            if (this.jornalistas.length !== 0){
                newId = Math.max(...this.jornalistas.map(j => j.id)) + 1;
            }

            this.jornalistas.push({
                id: newId,
                nome: this.nome,
                cpf: this.cpf,
                telefone: this.telefone
            });

            localStorage.setItem('jornalistas', JSON.stringify(this.jornalistas));
            
            alert('Jornalista cadastrado com sucesso');

            router.push('/nova-noticia');

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
