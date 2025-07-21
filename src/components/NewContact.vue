<template>
  <form @submit.prevent="submit" novalidate>
    <div class="field">
      <label class="label">Nombre</label>
      <div class="control">
        <input class="input" type="text" v-model="contact.name" :class="{ 'is-danger': errors.name }" required />
      </div>
      <p v-if="errors.name" class="help is-danger">Nombre es obligatorio</p>
    </div>

    <div class="field">
      <label class="label">Email</label>
      <div class="control">
        <input class="input" type="email" v-model="contact.email" :class="{ 'is-danger': errors.email }" required />
      </div>
      <p v-if="errors.email" class="help is-danger">Email inválido</p>
    </div>

    <div class="field">
      <label class="label">Dirección</label>
      <div class="control">
        <input class="input" type="text" v-model="contact.address" />
      </div>
    </div>

    <div class="field">
      <label class="label">Teléfono</label>
      <div class="control">
        <input class="input" type="tel" v-model="contact.phone" />
      </div>
    </div>

    <div class="field">
      <label class="label">País</label>
      <div class="control">
        <input class="input" type="text" v-model="contact.country" />
      </div>
    </div>

    <div class="field">
      <label class="label">Ciudad</label>
      <div class="control">
        <input class="input" type="text" v-model="contact.city" />
      </div>
    </div>

    <div class="field is-grouped is-grouped-right">
      <div class="control">
        <button type="submit" class="button is-primary">Guardar</button>
      </div>
      <div class="control">
        <button type="button" class="button" @click="$emit('cancel')">
          Cancelar
        </button>
      </div>
    </div>
  </form>
</template>

<script>
export default {
  name: "NewContact",
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
      errors: {},
    };
  },
  methods: {
    submit() {
      this.errors = {};
      if (!this.contact.name) this.errors.name = true;
      if (!this.isValidEmail(this.contact.email)) this.errors.email = true;

      if (Object.keys(this.errors).length) return;

      this.$emit("save", { ...this.contact });
    },
    isValidEmail(email) {
      const re = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
      return re.test(email);
    },
  },
};
</script>
