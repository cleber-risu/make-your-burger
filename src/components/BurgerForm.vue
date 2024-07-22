<script>
  export default {
    name: 'BurgerForm'
  }
</script>

<template>
  <div>
    <p>Componente de mensagem</p>
    <div>
      <form id="burger-form">
        <div class="input-container">
          <label for="name">Nome do cliente:</label>
          <input type="text" id="name" name="name" v-model="name" placeholder="Digite o seu nome">
        </div>
        <div class="input-container">
          <label for="bread">Escolha o pão:</label>
          <select name="bread" id="bread" v-model="bread">
            <option selected disabled>Selecione o seu pão</option>
            <option value=""></option>
          </select>
        </div>
        <div id="opcionais-container" class="input-container">
          <label id="opcionais-title" for="optional">Selecione os opcionais:</label>
          <div class="checkbox-container">
            <input type="checkbox" name="optional" v-model="optional" value="">
            <span>value</span>
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