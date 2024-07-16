<template>
  <q-layout view="lHh Lpr lFf">
    <q-header elevated>
      <q-toolbar>
        <q-btn
          flat
          dense
          round
          icon="menu"
          aria-label="Menu"
          @click="toggleLeftDrawer"
        />
        <img
          :src="carroauto"
          alt="logoautomundo"
          style="max-width: 20rem; max-height: 6rem"
        />
      </q-toolbar>
    </q-header>

    <q-drawer v-model="leftDrawerOpen" show-if-above bordered>
      <q-list>
        <q-item-label header><b>Filtros</b> </q-item-label>
        <q-input outlined v-model="filtronome" label="Nome" class="filtro" />
        <q-select
          outlined
          v-model="filtromarca"
          :options="optionsmarca"
          label="Marca"
          class="filtro"
        />
        <q-select
          outlined
          v-model="filtroano"
          :options="optionsano"
          label="Ano"
          class="filtro"
        />
        <q-select
          outlined
          v-model="filtroestado"
          :options="optionsestado"
          label="Estado"
          class="filtro"
        />
        <q-btn
          color="red"
          label="Limpar Filtros"
          @click="limpafiltros"
          class="limpar"
        />
      </q-list>
    </q-drawer>

    <q-page-container>
      <IndexPage :carlist="options" />
    </q-page-container>
  </q-layout>
</template>

<script>
import IndexPage from "src/pages/IndexPage.vue";
import { computed, defineComponent, ref, watch } from "vue";
import carroauto from "../assets/carroauto.png";
const carlist = [
  {
    Nome: "Fastback Abarth",
    Marca: "Fiat",
    Ano: 2023,
    Estado: "RS",
    Imagem:
      "https://cdn.motor1.com/images/mgl/1ZQ94w/s1/fiat-fastback-abarth---lancamento.jpg",
    Preco: 158000,
    Modelo: "1.3 TURBO 270 FLEX ABARTH AT6",
  },
  {
    Nome: "Tiguan",
    Marca: "Volkswagen",
    Ano: 2024,
    Estado: "RS",
    Imagem:
      "https://image.webmotors.com.br/_fotos/anunciousados/gigante/2024/202405/20240520/volkswagen-tiguan-2-0-300-tsi-gasolina-allspace-rline-automatico-wmimagem17240267027.webp?s=fill&w=249&h=186&q=70",
    Preco: 283000,
    Modelo: "1.3 TURBO 270 FLEX ABARTH AT6",
  },

  {
    Nome: "Fastback",
    Marca: "Fiat",
    Ano: 2023,
    Estado: "RS",
    Imagem:
      "https://garagem360.com.br/wp-content/uploads/2022/08/fastback-flagra-25.jpg",
    Preco: 125900,
    Modelo: "1.0 TURBO 200 FLEX IMPETUS CVT",
  },

  {
    Nome: "BMW X1",
    Marca: "BMW",
    Ano: 2021,
    Estado: "RS",
    Imagem:
      "https://http2.mlstatic.com/D_NQ_NP_771402-MLB77544423853_072024-O.webp",
    Preco: 219000,
    Modelo: "2.0 16V TURBO ACTIVEFLEX SDRIVE20I M SPORT 4P AUTOMÁTICO",
  },

  {
    Nome: "BMW X5",
    Marca: "BMW",
    Ano: 2019,
    Estado: "RS",
    Imagem:
      "https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcRDNLb-4jHSmJ-VFthXsJ0qzVFEisCuA0sZrw&s",
    Preco: 215000,
    Modelo: "3.0 M SPORT 4X4 30D I6 TURBO DIESEL 4P AUTOMÁTICO",
  },
];

const options = ref(carlist);
const filtromarca = ref("");
const filtroano = ref("");
const filtroestado = ref("");
const filtronome = ref("");

const aplicafiltros = () => {
  if (
    filtroano.value == "" &&
    filtroestado.value == "" &&
    filtromarca.value == "" &&
    filtronome.value == ""
  ) {
    options.value = carlist;
  } else {
    options.value = carlist.filter((e) => {
      return (
        (filtroano.value === "" || e.Ano == filtroano.value) &&
        (filtroestado.value === "" || e.Estado == filtroestado.value) &&
        (filtromarca.value === "" || e.Marca == filtromarca.value) &&
        (filtronome.value === "" ||
          e.Nome.toLowerCase().includes(filtronome.value.toLowerCase()))
      );
    });
  }
};
const limpafiltros = () => {
  filtroano.value = "";
  filtroestado.value = "";
  filtromarca.value = "";
  filtronome.value = "";
};
const optionsmarca = computed(() => {
  const valores = carlist.map((e) => e.Marca);
  return Array.from(new Set(valores));
});
const optionsano = computed(() => {
  const valores = carlist.map((e) => e.Ano.toString());
  return Array.from(new Set(valores));
});
const optionsestado = computed(() => {
  const valores = carlist.map((e) => e.Estado);
  return Array.from(new Set(valores));
});

export default defineComponent({
  name: "MainLayout",

  components: { IndexPage },

  setup() {
    const leftDrawerOpen = ref(false);
    watch([filtroano, filtroestado, filtromarca, filtronome], aplicafiltros, {
      immediate: true,
    });
    return {
      leftDrawerOpen,
      toggleLeftDrawer() {
        leftDrawerOpen.value = !leftDrawerOpen.value;
      },
      options,
      filtroano,
      filtroestado,
      filtromarca,
      filtronome,
      limpafiltros,
      optionsmarca,
      optionsestado,
      optionsano,
      carroauto,
    };
  },
});
</script>
<style scoped>
.filtro {
  margin: 0.5rem 1rem;
}
.limpar {
  width: 100%;
}
b {
  font-size: large;
}
</style>
