<template>
    <p>Componente de Mensagem</p>
    <div>
        <form id="potion-form">
            <div class="input-container">
                <label for="nome">Nome do Cliente</label>
                <input type="text" id="nome" name="name" v-model="nome" placeholder="Digite o seu nome:">
            </div>

            <div class="input-container">
                <label for="qualidade">Qualidade da Poção</label>
                <select name="qualidade" id="qualidade" v-model="qualidade">
                    <option value="">Selecione sua Poção</option>
                    <option v-for="qualidade in qualidades" :key="qualidade.id" :value="qualidade.tipo">
                        {{qualidade.tipo}}
                    </option>
                </select>
            </div>

            <div class="input-container">
                <label for="efeito">Efeito da Poção</label>
                <select name="efeito" id="efeito" v-model="efeito">
                    <option value="">Selecione o efeito:</option>
                    <option v-for="efeito in efeitos" :key="efeito.id" :value="efeito.tipo">
                        {{efeito.tipo}}
                    </option>
                </select>
            </div>

            <div id="opcionais-container" class="input-container">
                <label id="opcionais-title" for="opcionais">Efeitos Opcionais</label>
                <div class="checkbox-container" v-for="opcional in opcionaisData" :key="opcional.tipo">
                    <input type="checkbox" name="opcionais" v-model="opcionais" :value="opcional.tipo">
                    <span>{{opcional.tipo}}</span>
                </div>
            </div>

            <div class="input-container">
                <input type="submit" class="submit-btn" value="Criar minha Potion!">
            </div>
        </form>
    </div>
    
</template>

<script>
export default {
    name: 'PotionForm',
    data(){
        return {
            qualidades: null,
            efeitos: null,
            opcionaisData: null,
            nome: null,
            qualidade: null,
            efeito: null,
            opcionais: [],
            msg: null

        }
    },
    methods: {
        async getIngredientes() {
            const req = await fetch("http://localhost:3000/tipodepocao");
            const data = await req.json();

            this.qualidades = data.qualidade;
            this.efeitos = data.efeitos;
            this.opcionaisData = data.opcionais;

        }
    },
    mounted() {
        this.getIngredientes();
    }

}
</script>

<style scoped>
    #potion-form {
        max-width: 400px;
        margin: 0 auto;
    }

    .input-container {
        display: flex;
        flex-direction: column;
        margin-bottom: 20px;
    }

    label {
        font-weight: bold;
        margin-bottom: 15px;
        color: #222;
        padding: 5px 10px;
        border-left: 4px solid #03fc66;
    }

    input, select{
        padding: 5px 10px;
        width: 300px;
    }

    #opcionais-container{
        flex-direction: row;
        flex-wrap: wrap;
    }

    #opcionais-title {
        width: 100%;
    }

    .checkbox-container {
        display: flex;
        align-items: flex-start;
        width: 50%;
        margin-bottom: 20px;
    }

    .checkbox-container span,
    .checkbox-container input {
        width: auto;
    }

    .checkbox-container span{
        margin-left: 6px;
        font-weight: bold;
    }

    .submit-btn {
        background-color: #222;
        color: #03fc66;
        font-weight: bold;
        border: 2px solid #222;
        border-radius: 10px;
        padding: 10px;
        font-size: 16px;
        margin: 0 auto;
        cursor: pointer;
        transition: 0.5s;
    }

    .submit-btn:hover {
        background-color: transparent;
        color: #222;
    }
</style>