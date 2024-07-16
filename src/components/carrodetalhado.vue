<template>
  <q-dialog v-model="isOpen">
    <q-card class="car-detail-card">
      <q-card-section class="car-detail-header">
        <div class="text-h6">Detalhes do Carro</div>
      </q-card-section>

      <q-card-section class="car-detail-content">
        <img :src="carro.Imagem" alt="Imagem do Carro" class="car-image" />
        <div class="car-info">
          <p><strong>Nome:</strong> {{ carro.Nome }}</p>
          <p><strong>Ano:</strong> {{ carro.Ano }}</p>
          <p><strong>Marca:</strong> {{ carro.Marca }}</p>
          <p><strong>Modelo:</strong> {{ carro.Modelo }}</p>
          <p><strong>Estado:</strong> {{ carro.Estado }}</p>
        </div>
      </q-card-section>

      <q-card-actions align="right">
        <q-btn flat label="Fechar" color="primary" @click="closeDialog" />
      </q-card-actions>
    </q-card>
  </q-dialog>
</template>

<script>
import { ref, watch } from "vue";
import { defineComponent } from "vue";
export default defineComponent({
  name: "carroDetalhado",
  props: {
    carro: {
      type: Object,
      required: true,
    },
  },
  setup(props, { emit }) {
    const isOpen = ref(true);

    const closeDialog = () => {
      isOpen.value = false;
      emit("close");
    };

    watch(isOpen, (newVal) => {
      if (!newVal) {
        emit("close");
      }
    });

    return {
      isOpen,
      closeDialog,
    };
  },
});
</script>

<style scoped>
.car-detail-card {
  max-width: 400px;
  border-radius: 8px;
  overflow: hidden;
}

.car-detail-header {
  background-color: #f5f5f5;
  padding: 16px;
  text-align: center;
}

.car-detail-content {
  display: flex;
  flex-direction: column;
  align-items: center;
  padding: 16px;
}

.car-image {
  width: 100%;
  height: auto;
  border-radius: 4px;
  margin-bottom: 16px;
}

.car-info {
  text-align: left;
  width: 100%;
}

.car-info p {
  margin: 4px 0;
}
</style>
