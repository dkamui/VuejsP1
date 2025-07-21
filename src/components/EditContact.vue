<template>
  <form @submit.prevent="submit" novalidate>
    <div class="field">
      <label class="label">Nombre</label>
      <div class="control">
        <input class="input" type="text" v-model="contactData.name" :class="{ 'is-danger': errors.name }" required />
      </div>
      <p v-if="errors.name" class="help is-danger">Nombre es obligatorio</p>
    </div>

    <div class="field">
      <label class="label">Email</label>
      <div class="control">
        <input class="input" type="email" v-model="contactData.email" :class="{ 'is-danger': errors.email }" required />
      </div>
      <p v-if="errors.email" class="help is-danger">Email inválido</p>
    </div>

    <div class="field">
      <label class="label">Dirección</label>
      <div class="control">
        <input class="input" type="text" v-model="contactData.address" />
      </div>
    </div>

    <div class="field">
      <label class="label">Teléfono</label>
      <div class="control">
        <input class="input" type="tel" v-model="contactData.phone" />
      </div>
    </div>

    <div class="field">
      <label class="label">País</label>
      <div class="control">
        <input class="input" type="text" v-model="contactData.country" />
      </div>
    </div>

    <div class="field">
      <label class="label">Ciudad</label>
      <div class="control">
        <input class="input" type="text" v-model="contactData.city" />
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
  name: "EditContact",
  props: {
    contact: {
      type: Object,
      required: true,
    },
  },
  data() {
    return {
      contactData: { ...this.contact },
      errors: {},
    };
  },
  methods: {
    submit() {
      this.errors = {};
      if (!this.contactData.name) this.errors.name = true;
      if (!this.isValidEmail(this.contactData.email)) this.errors.email = true;

      if (Object.keys(this.errors).length) return;

      this.$emit("save", { ...this.contactData });
    },
    isValidEmail(email) {
      const re = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
      return re.test(email);
    },
  },
  watch: {
    contact(newVal) {
      this.contactData = { ...newVal };
      this.errors = {};
    },
  },
};
</script>
