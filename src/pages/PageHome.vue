<template>
  <div id="app">
    <nav class="orange darken-2">
      <div class="nav-wrapper"></div>
    </nav>
    <img alt="Vue logo" src="../assets/logo.png" width="32" />

    <div v-show="exibir.lista" style="padding 20px"></div>
    <button @click="mostrarCadastro">Cadastrar</button>

    <!-- Lista -->
    <div v-show="exibir.lista">
      <TarefaList
        msg="Welcome to Your Vue.js App"
        :tasks="listaDeTarefas"
      ></TarefaList>
    </div>

    <!-- FORM -->
    <div v-show="exibir.form">
      <h2>Cadastrar tarefa</h2>
      <input type="text" name="title" v-model="form.title" />
      <button class="btn" @click="salvarTarefa">SALVAR</button>
    </div>
  </div>
</template>

<script>
import TasksApi from "../TasksApi.js";

import TarefaList from "../components/TarefaList.vue";

export default {
  components: {
    TarefaList,
  },
  data: () => {
    return {
      listaDeTarefas: [],
      exibir: {
        lista: true,
        form: false,
      },
      form: {
        title: "",
      },
    };
  },
  methods: {
    listarTarefas() {
      TasksApi.getTasks((data) => {
        this.listaDeTarefas = data;
      });
    },
    mostrarCadastro() {
      this.exibir.lista = false;
      this.exibir.form = true;
    },
    salvarTarefa() {
      this.exibir.form = false;
      this.exibir.lista = true;
      const novaTarefa = {
        title: this.form.title,
        date: new Date().toLocaleDateString("pt"),
      };
      TasksApi.createTask(novaTarefa, () => {
        this.listarTarefas();
      });
    },
  },
  created() {
    this.listarTarefas();
  },
};
</script>

<style></style>
