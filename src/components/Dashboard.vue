<script>
  import Message from './Message.vue'

  export default {
    name: 'Dashboard',
    components: {
      Message
    },
    data() {
      return {
        burgers: null,
        burgerId: null,
        status: [],
        msg: null
      }
    },
    methods: {
      async getPedidos() {
        const req = await fetch('http://localhost:3000/burgers')
        const data = await req.json()
        this.burgers = data
      },
      async getStatus() {
        const req = await fetch('http://localhost:3000/status')
        const data = await req.json()
        this.status = data
      },
      async deleteBurger(id) {
        const req = await fetch(`http://localhost:3000/burgers/${id}`, {
          method: 'DELETE',
        })

        const res = await req.json()

        this.msg = `Pedido N°${res.id} removido com sucesso`

        setTimeout(() => this.msg = '', 5000)

        this.getPedidos()
      },
      async updateBurger(event, id) {
        const option = event.target.value
        const dataJson = JSON.stringify({ status: option })

        const req = await fetch(`http://localhost:3000/burgers/${id}`, {
          method: 'PATCH',
          headers: { 'Content-Type': 'application/json' },
          body: dataJson
        })

        const res = await req.json()

        this.msg = `Pedido N°${res.id} status atualizado para ${res.status}!`

        setTimeout(() => this.msg = '', 5000)

        console.log(res)
      }
    },
    mounted() {
      this.getPedidos()
      this.getStatus()
    }
  }
</script>

<template>
  <div class="burger-table">
    <Message :msg="msg" v-show="msg" />
    <div>
      <div id="burger-table-heading">
        <div class="order-id">#:</div>
        <div>Cliente:</div>
        <div>Pão:</div>
        <div>Carne:</div>
        <div>Opcionais:</div>
        <div>Ações</div>
      </div>
      <div id="burger-table-rows">
        <div class="burger-table-row" v-for="burger in burgers" :key="burger.id">
          <div class="order-number">{{ burger.id }}</div>
          <div>{{ burger.nome }}</div>
          <div>{{ burger.pao }}</div>
          <div>{{ burger.carne }}</div>
          <div>
            <ul>
              <li v-for="(opcional, index) in burger.opcionais" :key="index">{{ opcional }}</li>
            </ul>
          </div>
          <div>
            <select name="" class="status" @change="updateBurger($event, burger.id)">
              <option disabled>Selecione</option>
              <option v-for="st in status" :key="st.id" :value="st.tipo" :selected="burger.status == st.tipo">{{ st.tipo }}</option>
            </select>
            <button class="delete-btn" @click="deleteBurger(burger.id)">Cancelar</button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>

  #burger-table {
    max-width: 1200px;
    margin: 0 auto;
  }

  #burger-table-heading,
  #burger-table-rows,
  .burger-table-row {
    display: flex;
    flex-wrap: wrap;
  }

  #burger-table-heading {
    font-weight: bold;

    padding: 12px;

    border-bottom: 3px solid #333;
  }

  #burger-table-heading div,
  .burger-table-row div {
    width: 19%;
  }

  .burger-table-row {
    width: 100%;
    padding: 12px;

    border-bottom: 1px solid #ccc;
  }

  #burger-table-heading .order-id,
  .burger-table-row .order-number {
    width: 5%;
  }

  select {
    padding: 12px 6px;
    margin-right: 12px;
  }

  .delete-btn {
    background-color: #222;
    border: 2px solid #222;
    cursor: pointer;

    padding: 10px;
    margin: 0 auto;
    
    color: #fcba03;
    font-weight: bold;

    transition: 500ms;
  }

  .delete-btn:hover {
    background-color: transparent;
    color: #222;
  }

</style>