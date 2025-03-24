<template>
  <v-container>
    <h1 class="text-center">Tabela de Comparação de Preços</h1>
    <PriceComparisonTable :produtos="mockProdutos" />
  </v-container>
</template>

<script>
import PriceComparisonTable from '@/components/PriceComparisonTable.vue';
import { mockProdutos } from '@/mockData.js';

export default {
  name: 'HomeView',
  components: { PriceComparisonTable },
  data() {
    return { mockProdutos };
  }
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