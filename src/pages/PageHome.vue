<template>
  <div id="app">
    <img alt="Vue logo" src="../assets/logo.png" />
    <TarefaList msg="Welcome to Your Vue.js App" :tasks="listaDeTarefas" />
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
      listaDeTarefas: ["A", "B", "C"],
    };
  },
  created() {
    TasksApi.getTasks((data) => {
      this.listaDeTarefas = data;
    });
  },
};
</script>

<style></style>
