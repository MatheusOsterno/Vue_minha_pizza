<template>
    <p>Componente de mensagem</p>
    <div>
        <div id="pizza-form">
            <div class="input-container">
                <label for="nome">Nome do cliente: </label>
                <input type="text" id="nome" name="name" v-model="nome" placeholder="Digite o seu nome">
            </div>
            <div class="input-container">
                <label for="massa">Escolha o tamanho: </label>
                <select name="pao" id="pao" v-model="pao">
                    <option value="">Selecione a tamanho</option>
                    <option value="familia">Familia</option>
                </select>
            </div>
            <div class="input-container">
                <label for="massa">Escolha o pão: </label>
                <select name="pao" id="pao" v-model="pao">
                    <option value="">Selecione a massa</option>
                    <option value="farinha">Farinha de trigo</option>
                </select>
            </div>
            <div id="opcionais-container" class="input-container">
                <label id="opcionais-title" for="opcionais">Selecione os opcionais:</label>
                <div class="checkbox-container">
                    <input type="checkbox" name="opcionais" v-model="opcionais" value="salame">
                    <span>salame</span>   
                </div>
                <div class="checkbox-container">
                    <input type="checkbox" name="opcionais" v-model="opcionais" value="salame">
                    <span>salame</span>   
                </div>
                <div class="checkbox-container">
                    <input type="checkbox" name="opcionais" v-model="opcionais" value="salame">
                    <span>salame</span>   
                </div>
            </div>
            <div class="input-container">
                <input type="submit" class="submit-btn" value="Criar minha pizza">
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: "Pizzaform",
    data(){
        return {
            massas: null,
            tamanhos: null,
            opcionaisdata: null,
            nome: null,
            massa: null,
            tamanho: null,
            opcionais: [],
            status: "Solicitado",
            msng: null,
        }
    },
    methods: {
        async getIngredientes() {
            const req = await fetch("http://localhost:3000/ingredientes")
            const data = await req.json();

            console.log(data);
        }
    },
    mounted() {
        this.getIngredientes()
    }
}

</script>

<style scoped>
    #pizza-form {
        max-width: 400px ;
        margin: 0 auto;
    }

    .input-container{
        display: flex;
        flex-direction: column;
        margin-bottom: 20px;
    }

    label{
        font-weight: bold;
        margin-bottom: 15px;
        color: #222;
        padding: 5px 10px;
        border-left: 4px solid #fcba03;
    }

    input, select {
        padding: 5px 20px;
        width: 300px;
    }

    #opcionais-container{
        flex-direction: row;
        flex-wrap: wrap;
    }

    #opcionais-title{
        width: 100%;
    }

    .checkbox-container{
        display:flex;
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
        color: #fcba03;
        font-weight: bold;
        border: 2px solid #222;
        padding: 10px;
        font-size: 16px;
        margin: 0 auto;
        cursor: pointer;
        transition: 0.6s;
    }

    .submit-btn:hover {
        background-color: transparent;
        color: #222;

    }
</style>