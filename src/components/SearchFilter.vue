<template>
  <div>
    <h2>Filtrar Contactos</h2>
    <input v-model="nameFilter" placeholder="Filtrar por nombre" />
    <input v-model="emailFilter" placeholder="Filtrar por correo" />
    <button @click="applyFilters">Filtrar</button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      nameFilter: "Nombre",
      emailFilter: "Correo",
    };
  },
  methods: {
    applyFilters() {
      this.$emit("filter-contacts", {
        name: this.nameFilter,
        email: this.emailFilter,
      });
    },
  },
};
</script>
