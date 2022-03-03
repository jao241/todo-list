<template>
  <q-page class="column items-center q-mt-md">
    <h1 class="text-h5">Adicione algo a lista</h1>
    <q-input
      class="q-mb-md"
      label="Digite algo"
      v-model="state.texto"
    ></q-input>
    <div class="row q-mb-xl">
      <q-btn
        class="q-mr-sm"
        color="primary"
        text-color="white"
        label="Adicionar"
        @click="salvarTexto(state.texto)"
      ></q-btn>
      <q-btn
        v-if="state.temItens"
        color="primary"
        text-color="white"
        label="Limpar lista"
        @click="limparLista()"
      ></q-btn>
    </div>
    <q-list
      class="row justify-around q-mt-sm text-center bg-indigo-2 q-pa-sm"
      style="width: 80%; border-radius: 1px"
      v-for="(itemDaLista, index) of lista"
      :key="index"
    >
      <q-item class="row full-width">
        <p class="col-11">{{ itemDaLista }}</p>
        <div>
          <q-icon
            class="bg-green-2 q-pa-sm q-mr-sm"
            name="check"
            color="green"
            size="20px"
            @click="adicionarAListaConcluida(itemDaLista, index)"
            style="border-radius: 50%; cursor: pointer"
          ></q-icon>
          <q-icon
            class="bg-red-2 q-pa-sm"
            name="remove"
            color="red"
            size="20px"
            @click="removerItem(itemDaLista, index)"
            style="border-radius: 50%; cursor: pointer"
          ></q-icon>
        </div>
      </q-item>
    </q-list>
  </q-page>
</template>

<script>
import { defineComponent, ref } from "vue";

export default defineComponent({
  name: "PageIndex",
  setup() {
    const state = ref({
      texto: "",
      temItens: false,
    });

    const lista = ref([
      "Um item padrão que não será removido quando a página recarregar!",
    ]);
    const listaConcluida = ref([]);
    // const listaRemovida = ref([]);

    function salvarTexto(texto) {
      if (texto.length > 0) {
        lista.value.unshift(texto);
        state.value.temItens = true;
      } else
        alert("Por favor digite algo para que possa ser adicionado a lista!");
    }

    function limparLista() {
      lista.value = [];
      state.value.temItens = false;
    }

    function removerItem(itemDaLista, index) {
      lista.value.splice(index, 1);
      lista.value.length > 0 ? true : (state.value.temItens = false);
    }

    function adicionarAListaConcluida(itemDaLista, index) {
      listaConcluida.value.unshift(itemDaLista);
      removerItem(itemDaLista, index);
    }

    return {
      state,
      lista,
      salvarTexto,
      limparLista,
      removerItem,
      adicionarAListaConcluida,
    };
  },
});
</script>
