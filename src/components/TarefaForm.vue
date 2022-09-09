<template>
  <div>
    <h2>Cadastrar tarefa</h2>
    <input
      type="text"
      name="title"
      placeholder="Entre com a tarefa"
      v-model="form.title"
    />
    <input
      type="text"
      name="project"
      placeholder="Entre com o projeto"
      v-model="form.project"
    />
    <button class="btn" @click="salvarTarefa">SALVAR</button>
  </div>
</template>

<script>
export default {
  props: ["titulo"],
  data: () => {
    return {
      form: {
        title: "",
        project: "",
      },
    };
  },
  methods: {
    salvarTarefa() {
      const novaTarefa = {
        title: this.form.title,
        project: this.form.project,
        date: new Date().toLocaleDateString("pt"),
      };
      this.$emit("salvarClick", novaTarefa);
    },
  },
};
</script>
