<template>
  <div class="container">
    <h1 class="title">{{ title }}</h1>

    <button class="button is-primary mb-4" @click="openModal('crear')">
      Nuevo
    </button>

    <div class="field mb-4">
      <label class="label">Filtrar por país</label>
      <div class="control">
        <div class="select is-fullwidth">
          <select v-model="filtros.pais">
            <option value="">Todos los países</option>
            <option v-for="pais in paisesDisponibles" :key="pais" :value="pais">
              {{ pais }}
            </option>
          </select>
        </div>
      </div>
    </div>

    <div class="field mb-5">
      <label class="label">Buscar por nombre o email</label>
      <div class="control">
        <input class="input" type="text" placeholder="Escribe nombre o email" v-model="filtros.texto" />
      </div>
    </div>
    <div class="table-container">
      <table class="table is-fullwidth is-striped is-hoverable">
        <thead>
          <tr>
            <th>id</th>
            <th>Nombre</th>
            <th>Email</th>
            <th>Dirección</th>
            <th>Teléfono</th>
            <th>País</th>
            <th>Ciudad</th>
            <th></th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="(contact) in filteredContacts" :key="contact.id">
            <td>{{ contact.id }}</td>
            <td>{{ contact.name }}</td>
            <td>{{ contact.email }}</td>
            <td>{{ contact.address }}</td>
            <td>{{ contact.phone }}</td>
            <td>{{ contact.country }}</td>
            <td>{{ contact.city }}</td>
            <td>
              <button class="button is-small is-info mr-2" @click="openModal('editar', contact.id)">
                Editar
              </button>
              <button class="button is-small is-danger" @click="deleteContact(contact.id)">
                Eliminar
              </button>
            </td>
          </tr>
        </tbody>
      </table>
    </div>
    <!-- Modal Bulma -->
    <div :class="['modal', isModalActive ? 'is-active' : '']">
      <div class="modal-background" @click="closeModal"></div>
      <div class="modal-card" style="width: 600px; max-width: 95%">
        <header class="modal-card-head">
          <p class="modal-card-title">{{ modalTitle }}</p>
          <button class="delete" aria-label="close" @click="closeModal"></button>
        </header>
        <section class="modal-card-body">
          <EditContact v-if="modalMode === 'editar'" :contact="selectedContact" @save="updateContact"
            @cancel="closeModal" />
          <NewContact v-if="modalMode === 'crear'" @save="addContact" @cancel="closeModal" />
        </section>
      </div>
    </div>
  </div>
</template>

<script>
import EditContact from "../components/EditContact.vue";
import NewContact from "../components/NewContact.vue";

export default {
  name: "ContactsView",
  components: { EditContact, NewContact },
  data() {
    return {
      title: "Contactos",
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
          name: "Bob Smith",
          email: "bob.smith@example.com",
          address: "456 Oak Avenue",
          phone: "987-654-3210",
          country: "Canada",
          city: "Toronto",
        },
        {
          id: 3,
          name: "Carol White",
          email: "carol.white@example.com",
          address: "789 Pine Road",
          phone: "555-123-4567",
          country: "UK",
          city: "London",
        },
        {
          id: 4,
          name: "David Brown",
          email: "david.brown@example.com",
          address: "321 Elm Street",
          phone: "444-555-6666",
          country: "Australia",
          city: "Sydney",
        },
        {
          id: 5,
          name: "Emily Davis",
          email: "emily.davis@example.com",
          address: "654 Spruce Lane",
          phone: "333-444-5555",
          country: "USA",
          city: "Los Angeles",
        },
        {
          id: 6,
          name: "Frank Miller",
          email: "frank.miller@example.com",
          address: "987 Cedar Blvd",
          phone: "222-333-4444",
          country: "Germany",
          city: "Berlin",
        },
        {
          id: 7,
          name: "Grace Lee",
          email: "grace.lee@example.com",
          address: "123 Birch St",
          phone: "555-666-7777",
          country: "South Korea",
          city: "Seoul",
        },
        {
          id: 8,
          name: "Hannah Kim",
          email: "hannah.kim@example.com",
          address: "456 Willow Dr",
          phone: "888-999-0000",
          country: "South Korea",
          city: "Busan",
        },
        {
          id: 9,
          name: "Ian Clark",
          email: "ian.clark@example.com",
          address: "789 Aspen Way",
          phone: "777-888-9999",
          country: "USA",
          city: "Chicago",
        },
        {
          id: 10,
          name: "Jane Foster",
          email: "jane.foster@example.com",
          address: "321 Redwood Rd",
          phone: "666-777-8888",
          country: "Canada",
          city: "Vancouver",
        },
        {
          id: 11,
          name: "Kyle Green",
          email: "kyle.green@example.com",
          address: "654 Pine St",
          phone: "555-444-3333",
          country: "UK",
          city: "Manchester",
        },
        {
          id: 12,
          name: "Laura Scott",
          email: "laura.scott@example.com",
          address: "123 Oak Ln",
          phone: "444-333-2222",
          country: "Australia",
          city: "Melbourne",
        },
        {
          id: 13,
          name: "Mike Adams",
          email: "mike.adams@example.com",
          address: "456 Elm St",
          phone: "333-222-1111",
          country: "USA",
          city: "Houston",
        },
        {
          id: 14,
          name: "Nina Patel",
          email: "nina.patel@example.com",
          address: "789 Maple Ave",
          phone: "222-111-0000",
          country: "India",
          city: "Mumbai",
        },
        {
          id: 15,
          name: "Oscar Martinez",
          email: "oscar.martinez@example.com",
          address: "321 Cedar St",
          phone: "111-000-9999",
          country: "Mexico",
          city: "Mexico City",
        },
        {
          id: 16,
          name: "Paula Ruiz",
          email: "paula.ruiz@example.com",
          address: "654 Birch Rd",
          phone: "000-999-8888",
          country: "Spain",
          city: "Madrid",
        },
        {
          id: 17,
          name: "Quentin Blake",
          email: "quentin.blake@example.com",
          address: "123 Willow St",
          phone: "999-888-7777",
          country: "France",
          city: "Paris",
        },
        {
          id: 18,
          name: "Rachel Kim",
          email: "rachel.kim@example.com",
          address: "456 Aspen Blvd",
          phone: "888-777-6666",
          country: "South Korea",
          city: "Daegu",
        },
        {
          id: 19,
          name: "Steve Rogers",
          email: "steve.rogers@example.com",
          address: "789 Redwood Dr",
          phone: "777-666-5555",
          country: "USA",
          city: "San Francisco",
        },
        {
          id: 20,
          name: "Tina Chen",
          email: "tina.chen@example.com",
          address: "321 Spruce Ln",
          phone: "666-555-4444",
          country: "China",
          city: "Beijing",
        },
      ],
      filtros: {
        pais: "",
        texto: "",
      },
      isModalActive: false,
      modalMode: null,
      selectedIndex: null,
      selectedContact: null,
    };
  },
  computed: {
    paisesDisponibles() {
      return [...new Set(this.contacts.map((c) => c.country))].sort();
    },
    filteredContacts() {
      return this.contacts.filter((c) => {
        const filtroPais = this.filtros.pais;
        const filtroTexto = this.filtros.texto.toLowerCase();

        const coincidePais = filtroPais ? c.country === filtroPais : true;
        const coincideTexto =
          !filtroTexto ||
          c.name.toLowerCase().includes(filtroTexto) ||
          c.email.toLowerCase().includes(filtroTexto);

        return coincidePais && coincideTexto;
      });
    },
    modalTitle() {
      return this.modalMode === "editar" ? "Editar Contacto" : "Nuevo Contacto";
    },
  },
  methods: {
    openModal(mode, id = null) {
      this.modalMode = mode;
      if (mode === "editar" && id !== null) {
        const contact = this.contacts.find(c => c.id === id);
        this.selectedIndex = this.contacts.findIndex(c => c.id === id);
        this.selectedContact = { ...contact };
      } else {
        this.selectedContact = null;
        this.selectedIndex = null;
      }
      this.isModalActive = true;
    },
    closeModal() {
      this.isModalActive = false;
      this.selectedContact = null;
      this.selectedIndex = null;
      this.modalMode = null;
    },
    updateContact(updatedContact) {
      if (this.selectedIndex !== null) {
        this.contacts.splice(this.selectedIndex, 1, updatedContact);
      }
      this.closeModal();
    },
    addContact(newContact) {
      const maxId = this.contacts.length
        ? Math.max(...this.contacts.map((c) => c.id))
        : 0;
      newContact.id = maxId + 1;
      this.contacts.push(newContact);
      this.closeModal();
    },
    deleteContact(id) {
      const index = this.contacts.findIndex(c => c.id === id);
      if (confirm(`¿Está seguro de eliminar el contacto ${this.contacts[index].name}, id: ${id}?`)) {
        this.contacts.splice(index, 1);
      }
    },
  },
};
</script>
