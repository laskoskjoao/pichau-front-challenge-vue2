<template>
  <div class="home">
    <div class="container">
      <h1>Desafio Vue.js - Tabela de Comparação de Preços</h1>
      <p>Implemente o componente <code>PriceComparisonTable</code> conforme as especificações.</p>
    </div>
  </div>
</template>

<script>
export default {
  name: 'HomeView'
};
</script>

<style scoped>
.home {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
  background-color: #0080ff50;
  text-align: center;
}
.container {
  max-width: 600px;
  padding: 20px;
  background: white;
  border-radius: 10px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
}
</style>