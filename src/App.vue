<!-- eslint-disable prettier/prettier -->
<!-- eslint-disable prettier/prettier -->
<!-- eslint-disable prettier/prettier -->
<template>
  <div id="app">
    <h1>Agenda de Contactos</h1>
    <SearchFilter @filter-contacts="filterContacts" />
    <ContactForm :editContact="currentContact" @save-contact="saveContact" />
    <ContactList
      :contacts="filteredContacts"
      @edit-contact="editContact"
      @delete-contact="deleteContact"
    />
    </div>
</template>

<script>
import ContactList from "./components/ContactList.vue";
import ContactForm from "./components/ContactForm.vue";
import SearchFilter from "./components/SearchFilter.vue";

export default {
  components: {
    ContactList,
    ContactForm,
    SearchFilter,
  },
  data() {
    return {
      contacts: [
        {
          id: 1,
          name: "Alice Johnson",
          email: "alice.johnson@example.com",
          address: "123 Maple Street",
          phone: "123-456-7890",
          country: "USA",
          city: "New York",
        },
        {
          id: 2,
          name: "Carol White",
          email: "carol.white@example.com",
          address: "789 Pine Road",
          phone: "555-123-4567",
          country: "UK",
          city: "London",
        },
        {
          id: 3,
          name: "Bob Smith",
          email: "bob.smith@example.com",
          address: "456 Oak Avenue",
          phone: "987-654-3210",
          country: "Canada",
          city: "Toronto",
        },
        {
          id: 4,
          name: "Carol White",
          email: "carol.white@example.com",
          address: "789 Pine Road",
          phone: "555-123-4567",
          country: "UK",
          city: "London",
        },
      ],
      filteredContacts: [],
      currentContact: null,
    };
  },
  created() {
    this.filteredContacts = this.contacts;
  },
  methods: {
    filterContacts(filters) {
      this.filteredContacts = this.contacts.filter(
        (contact) =>
          contact.name.includes(filters.name) &&
          contact.email.includes(filters.email)
      );
    },
    editContact(contact) {
      this.currentContact = contact;
    },
    saveContact(contact) {
      if (contact.id) {
        const index = this.contacts.findIndex((c) => c.id === contact.id);
        this.contacts.splice(index, 1, contact);
      } else {
        contact.id = Date.now();
        this.contacts.push(contact);
      }
      this.filteredContacts = this.contacts;
      this.currentContact = null;
    },
    deleteContact(id) {
      this.contacts = this.contacts.filter((contact) => contact.id !== id);
      this.filteredContacts = this.contacts;
    },
  },
};
</script>
