<template>
    <v-container>
        <v-data-table
            :headers="headers"
            :items="produtos"
            :items-per-page="20"
            class="elevation-2"
        >
            <template v-slot:item="props">
                <tr>
                    <!-- nome -->
                    <td>
                        {{ props.item.nome }}
                    </td>

                    <!-- preço -->
                    <td>
                        {{ props.item.preco }}
                    </td>

                    <!-- concorrentes -->
                    <td
                        v-for="fornecedor in fornecedores"
                            :key="fornecedor"
                            :class="getPriceClass(props.item.concorrentes[fornecedor], props.item)"
                        >
                            {{ props.item.concorrentes[fornecedor] ? formatPrice(props.item.concorrentes[fornecedor]) : 'N/A' }}
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
    getPriceClass(preco, produto) {
        if (preco === undefined) return '';
            const precos = [produto.preco, ...Object.values(produto.concorrentes)].filter(p => p !== undefined);
            const min = Math.min(...precos);
            const max = Math.max(...precos);

            if (preco === min) return 'min-price';
            if (preco === max) return 'max-price';
            return '';
        },
        formatPrice(value) {
            return value ? `R$ ${value}` : 'N/A';
        }
    }
};
</script>

<style>
.bold {
  font-weight: bold;
}

.min-price {
  color: green;
}

.max-price {
  color: red;
}
</style>
