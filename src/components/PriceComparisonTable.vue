<template>
    <v-container>
        <v-data-table
            :headers="headers"
            :items="produtos"
            :items-per-page="20"
            class="elevation-2"
        >
            <template v-slot:item="produtos">
                <tr>
                <!-- nome -->
                <td>
                    {{ produtos.item.nome }}
                </td>

                <!-- preço -->
                <td>
                    {{ produtos.item.preco }}
                </td>

                <!-- concorrentes -->
                <td v-for="fornecedor in fornecedores" :key="fornecedor">
                    {{ produtos.item.concorrentes[fornecedor] ? produtos.item.concorrentes[fornecedor] : 'N/A' }}
                </td>
                </tr>
            </template>
        </v-data-table>
    </v-container>
</template>

<script>
export default {
  props: {
    produtos: Array
  },
  computed: {
    fornecedores() {
      //obtém fornecedores únicos da lista de produtos
      const fornecedoresSet = new Set();
      this.produtos.forEach(produto => {
        Object.keys(produto.concorrentes).forEach(fornecedor => fornecedoresSet.add(fornecedor));
      });
      return Array.from(fornecedoresSet);
    },
    headers() {
      return [
        { text: "Produto", value: "nome" },
        { text: "Preço Empresa", value: "preco" },
        ...this.fornecedores.map(fornecedor => ({
          text: fornecedor,
          value: fornecedor
        }))
      ];
    }
  },
  methods: {
  }
};
</script>

<style>
</style>
