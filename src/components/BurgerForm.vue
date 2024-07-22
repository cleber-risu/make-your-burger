<script>
  export default {
    name: 'BurgerForm',
    data() {
      return {
        breads: null,
        meats: null,
        optionalData: null,
        name: null,
        bread: null,
        meat: null,
        optionals: [],
        msg: null
      }
    },
    methods: {
      async getIngredients() {
        const req = await fetch('http://localhost:3000/ingredientes')
        const data = await req.json();
        
        this.breads = data.paes
        this.meats = data.carnes
        this.optionalData = data.opcionais
      },
      async createBurger(event) {
        event.preventDefault();
        
        const data = {
          nome: this.name,
          carne: this.meat,
          pao: this.bread,
          opcionais: [...this.optionals],
          status: 'Solicitado'
        }

        const dataJson = JSON.stringify(data)

        const req = await fetch('http://localhost:3000/burgers', {
          method: 'POST',
          headers: { 'Content-Type': 'application/json' },
          body: dataJson
        })

        const res = await req.json();

        // todo - colocar uma msg do sistema

        // todo - limpar mensagem

        this.name = ''
        this.meat = ''
        this.bread = ''
        this.optionals = ''
      }
    },
    mounted() {
      this.getIngredients()
    }
  }
</script>

<template>
  <div>
    <p>Componente de mensagem</p>
    <div>
      <form id="burger-form" @submit="createBurger($event)">

        <div class="input-container">
          <label for="name">Nome do cliente:</label>
          <input type="text" id="name" name="name" v-model="name" placeholder="Digite o seu nome">
        </div>

        <div class="input-container">
          <label for="bread">Escolha o pão:</label>
          <select name="bread" id="bread" v-model="bread">
            <option selected disabled>Selecione o seu pão</option>
            <option v-for="bread in breads" :key="bread.id" :value="bread.tipo">
              {{ bread.tipo }}
            </option>
          </select>
        </div>

        <div class="input-container">
          <label for="meat">Escolha a carne:</label>
          <select name="meat" id="meat" v-model="meat">
            <option selected disabled>Selecione a sua carne</option>
            <option v-for="meat in meats" :key="meat.id" :value="meat.tipo">
              {{ meat.tipo }}
            </option>
          </select>
        </div>

        <div id="opcionais-container" class="input-container">
          <label id="opcionais-title" for="optional">Selecione os opcionais:</label>
          <div class="checkbox-container" v-for="optional in optionalData" :key="optional.id">
            <input type="checkbox" name="optional" v-model="optionals" :value="optional.tipo">
            <span>{{ optional.tipo }}</span>
          </div>
        </div>

        <div class="input-container">
          <input type="submit" value="Criar meu Burger" class="submit-btn">
        </div>

      </form>
    </div>
  </div>
</template>

<style scoped>

  #burger-form {
    max-width: 400px;
    margin: 0 auto;
  }

  .input-container {
    display: flex;
    flex-direction: column;

    margin-bottom: 14px;
  }

  label {
    color: #222;
    font-weight: bold;

    margin-bottom: 10px;
    padding: 5px 10px;

    border-left: 4px solid #fcba03;
  }

  input, select {
    padding: 5px 10px;
    width: 300px;
  }

  #opcionais-container {
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

  .checkbox-container span {
    margin-left: 6px;
    font-weight: bold;
  }

  .submit-btn {
    background-color: #222;
    border: 2px solid #222;
    cursor: pointer;

    padding: 10px;
    /* margin: 0 auto; */

    color: #fcba03;
    font-size: 16px;
    font-weight: bold;

    transition: 500ms;
  }

  .submit-btn:hover {
    background-color: transparent;
    color: #222;
  }

</style>