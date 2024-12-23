<template>
  <div>
    <h2>{{ editMode ? "Editar Contacto" : "Agregar Contacto" }}</h2>
    <form @submit.prevent="handleSubmit">
      <input v-model="contact.name" placeholder="Nombre" required />
      <input v-model="contact.email" placeholder="Correo" required />
      <input v-model="contact.address" placeholder="Dirección" />
      <input v-model="contact.phone" placeholder="Teléfono" />
      <input v-model="contact.country" placeholder="País" />
      <input v-model="contact.city" placeholder="Ciudad" />
      <button type="submit">Guardar</button>
    </form>
  </div>
</template>

<script>
export default {
  props: {
    editContact: {
      type: Object,
      default: null,
      validator(value) {
        return value === null || (typeof value === "object" && value !== null);
      },
    },
  },
  data() {
    return {
      contact: {
        name: "",
        email: "",
        address: "",
        phone: "",
        country: "",
        city: "",
      },
    };
  },
  computed: {
    editMode() {
      return !!this.editContact;
    },
  },
  watch: {
    editContact: {
      immediate: true,
      handler(newContact) {
        this.contact = newContact
          ? { ...newContact }
          : {
              name: "",
              email: "",
              address: "",
              phone: "",
              country: "",
              city: "",
            };
      },
    },
  },
  methods: {
    handleSubmit() {
      this.$emit("save-contact", { ...this.contact });
      this.resetForm();
    },
    resetForm() {
      this.contact = {
        name: "",
        email: "",
        address: "",
        phone: "",
        country: "",
        city: "",
      };
    },
  },
};
</script>
