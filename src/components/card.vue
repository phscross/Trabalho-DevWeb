<template>
  <div class="car-card">
    <img :src="imagem" alt="Car Image" class="car-image" />
    <div class="car-details">
      <h2 class="car-title">{{ nome }}</h2>
      <p class="car-description">Modelo: {{ modelo }}</p>
      <p class="car-description">Ano: {{ ano }}</p>
      <p class="car-price">R$ {{ preco }}</p>
      <p class="car-description">Marca: {{ marca }}</p>
      <p class="car-description">Estado: {{ estado }}</p>
    </div>
  </div>
</template>
<script>
import { defineComponent } from "vue";

export default defineComponent({
  name: "CardPrincipal",
  props: {
    marca: {
      type: String,
      required: true,
    },

    nome: {
      type: String,
      required: true,
    },

    imagem: {
      type: String,
      default: "",
    },

    ano: {
      type: Number,
      default: 1900,
    },
    preco: {
      type: Number,
      default: 0,
    },

    estado: {
      type: String,
      default: "",
    },

    modelo: {
      type: String,
      default: "",
    },
  },
});
</script>
<style scoped>
.car-card {
  border: 1px solid #ddd;
  border-radius: 8px;
  overflow: hidden;
  box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
  max-width: 300px;
  margin: 20px;
}

.car-image {
  width: 100%;
  height: auto;
  display: block;
}

.car-details {
  padding: 15px;
}

.car-title {
  font-size: 1.5em;
  margin: 0;
  color: #333;
}

.car-description {
  font-size: 1em;
  color: #666;
  margin: 10px 0;
}

.car-price {
  font-size: 1.2em;
  color: #27ae60;
  font-weight: bold;
}
</style>
