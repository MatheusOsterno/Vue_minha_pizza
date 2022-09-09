<template>
    <Message :msg="msg" v-show="msg" />
    <div>
        <form id="pizza-form" @submit="createPizza" >
            <div class="input-container">
                <label for="nome">Nome do cliente: </label>
                <input type="text" id="nome" name="name" v-model="nome" placeholder="Digite o seu nome">
            </div>
            <div class="input-container">
                <label for="massa">Escolha o tamanho: </label>
                <select name="pao" id="pao" v-model="tamanho">
                    <option value="">Selecione a tamanho</option>
                    <option :value="tamanho.tipo" v-for="tamanho in tamanhos" :key="tamanho.id">
                        {{ tamanho.tipo }}
                    </option>
                </select>
            </div>
            <div class="input-container">
                <label for="massa">Escolha o massa: </label>
                <select name="pao" id="pao" v-model="massa">
                    <option value="">Selecione a massa</option>
                    <option :value="massa.tipo" v-for="massa in massas" :key="massa.id">
                        {{ massa.tipo }}
                    </option>
                </select>
            </div>
            <div id="opcionais-container" class="input-container">
                <label id="opcionais-title" for="opcionais">Selecione os opcionais:</label>
                <div class="checkbox-container" v-for="opcional in opcionaisdata" :key="opcional.id">
                    <input type="checkbox" name="opcionais" v-model="opcionais" :value="opcional.tipo">
                    <span>{{ opcional.tipo }}</span> 
                </div>

            </div>
            <div class="input-container">
                <input type="submit" class="submit-btn" value="Criar minha pizza">
            </div>
        </form>
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
            msng: null,
        }
    },
    methods: {
        async getIngredientes() {
            const req = await fetch("http://localhost:3000/ingredientes")
            const data = await req.json();

            this.massas = data.massas;
            this.tamanhos = data.tamanhos;
            this.opcionaisdata = data.opcionais
        },
        async createPizza(e) {
            e.preventDefault();
            const data = {
                nome: this.nome,
                massa: this.massa,
                tamanho: this.tamanho,
                opcionais: Array.from(this.opcionais),
                status: "Solicitado",
            }

            const dataJson = JSON.stringify(data)    

            const req = await fetch("http://localhost:3000/pizzas", {
                method: "POST",
                headers: { "Content-Type" : "application/json" },
                body: dataJson
            });
            const res = await req.json()
            console.log(res)

            //criar mensagem
            this.msg = "Pedido realizado com sucesso!"

            //Limpar campo
            this.nome = "";
            this.massa = "";
            this.tamanho= "";
            this.opcionais= "";


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