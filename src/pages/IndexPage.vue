<template>
  <q-page class="flex flex-center">
    <div
      v-for="(carro, index) in carlist"
      :key="index"
      @click="selecionacarro(carro)"
      class="cardcarro"
    >
      <CardPrincipal
        :nome="carro.Nome"
        :ano="carro.Ano"
        :estado="carro.Estado"
        :marca="carro.Marca"
        :imagem="carro.Imagem"
        :preco="carro.Preco"
        :modelo="carro.Modelo"
      />
    </div>
    <carroDetalhado
      v-if="carroselecionado"
      :carro="carroselecionado"
      @close="carroselecionado = null"
    />
  </q-page>
</template>

<script>
import { defineComponent, ref } from "vue";
import CardPrincipal from "../components/card.vue";
import carroDetalhado from "../components/carrodetalhado.vue";
const carroselecionado = ref(null);
const selecionacarro = (carro) => {
  console.log(carro);
  carroselecionado.value = carro;
};

export default defineComponent({
  name: "IndexPage",

  props: {
    carlist: {
      type: Object,
      required: true,
    },
  },

  components: { CardPrincipal, carroDetalhado },
  setup() {
    return {
      carroselecionado,
      selecionacarro,
    };
  },
});
</script>
<style scoped>
.cardcarro:hover {
  transform: scale(1.1);
  cursor: pointer;
}
</style>
