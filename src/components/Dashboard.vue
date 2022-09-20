
<template>
  <div id="pizzas-table" v-if="pizzass">
    <div>
      <div id="pizzas-table-heading">
        <div class="order-id">#:</div>
        <div>Cliente:</div>
        <div>Pão:</div>
        <div>tamanho:</div>
        <div>Opcionais:</div>
        <div>Ações:</div>
      </div>
    </div>
    <div id="pizzas-table-rows">
      <div class="pizzas-table-row" v-for="pizzas in pizzass" :key="pizzas.id">
        <div class="order-number">{{ pizzas.id }}</div>
        <div>{{ pizzas.nome }}</div>
        <div>{{ pizzas.massa }}</div>
        <div>{{ pizzas.tamanho }}</div>
        <div>
          <ul v-for="(opcional, index) in pizzas.opcionais" :key="index">
            <li>{{ opcional }}</li>
          </ul>
        </div>
        <div>
          <select name="status" class="status" @change="updatepizzas($event, pizzas.id)">
            <option :value="s.tipo" v-for="s in status" :key="s.id" :selected="pizzas.status == s.tipo">
              {{ s.tipo }}
            </option>
          </select>
          <button class="delete-btn" @click="deletepizzas(pizzas.id)">Cancelar</button>
        </div>
      </div>
    </div>
  </div>
  <div v-else>
    <h2>Não há pedidos no momento!</h2>
  </div>
</template>
<script>
  export default {
    name: "Dashboard",
    data() {
      return {
        pizzass: null,
        pizzas_id: null,
        status: []
      }
    },
    methods: {
      async getPedidos() {
        const req = await fetch('http://localhost:3000/pizzas')
        const data = await req.json()
        this.pizzass = data
        // Resgata os status de pedidos
        this.getStatus()
      },
      async getStatus() {
        const req = await fetch('http://localhost:3000/status')
        const data = await req.json()
        this.status = data
      },
      async deletepizzas(id) {
        const req = await fetch(`http://localhost:3000/pizzas/${id}`, {
          method: "DELETE"
        });
        const res = await req.json()
        this.getPedidos()
      },
      async updatepizzas(event, id) {
        const option = event.target.value;
        const dataJson = JSON.stringify({status: option});
        const req = await fetch(`http://localhost:3000/pizzas/${id}`, {
          method: "PATCH",
          headers: { "Content-Type" : "application/json" },
          body: dataJson
        });
        const res = await req.json()
        console.log(res)
      }
    },
    mounted () {
    this.getPedidos()
    }
  }
</script>

<style scoped>
  #pizzas-table {
    max-width: 1200px;
    margin: 0 auto;
  }
  #pizzas-table-heading,
  #pizzas-table-rows,
  .pizzas-table-row {
    display: flex;
    flex-wrap: wrap;
  }
  #pizzas-table-heading {
    font-weight: bold;
    padding: 12px;
    border-bottom: 3px solid #333;
  }
  .pizzas-table-row {
    width: 100%;
    padding: 12px;
    border-bottom: 1px solid #CCC;
  }
  #pizzas-table-heading div,
  .pizzas-table-row div {
    width: 19%;
  }
  #pizzas-table-heading .order-id,
  .pizzas-table-row .order-number {
    width: 5%;
  }
  select {
    padding: 12px 6px;
    margin-right: 12px;
  }
  .delete-btn {
    background-color: #222;
    color:#fcba03;
    font-weight: bold;
    border: 2px solid #222;
    padding: 10px;
    font-size: 16px;
    margin: 0 auto;
    cursor: pointer;
    transition: .5s;
  }
  
  .delete-btn:hover {
    background-color: transparent;
    color: #222;
  }
  
</style>