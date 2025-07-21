<template>
  <section class="section has-background-light">
    <div class="container has-text-centered">
      <h2 class="title is-3">Práctica 1 - Vue 3</h2>
      <p class="subtitle is-5">
        Aplicación web para gestión de contactos personales
      </p>
      <a href="/contacts" class="button is-primary is-medium mt-4">Ingresar a la app</a>
    </div>
  </section>

  <section class="section">
    <div class="container">
      <h3 class="title is-4 has-text-centered">Descripción del proyecto</h3>
      <p class="mt-4">
        Esta aplicación permite guardar, visualizar, filtrar y administrar
        contactos personales. Cada contacto contiene los siguientes campos:
      </p>
      <ul class="mt-3">
        <li>✔️ ID</li>
        <li>✔️ Nombre</li>
        <li>✔️ Correo electrónico</li>
        <li>✔️ Dirección</li>
        <li>✔️ Teléfono</li>
        <li>✔️ País</li>
        <li>✔️ Ciudad</li>
      </ul>
    </div>
  </section>

  <section class="section has-background-light">
    <div class="container">
      <h3 class="title is-4 has-text-centered">Funciones implementadas</h3>
      <ul class="mt-4">
        <li>✔️ Listar contactos</li>
        <li>✔️ Agregar nuevo contacto</li>
        <li>✔️ Editar contacto existente</li>
        <li>✔️ Eliminar contacto</li>
        <li>✔️ Filtrado combinado por nombre y/o correo electrónico</li>
        <li>✔️ Filtrado dinámico por país basado en los contactos cargados</li>
      </ul>
    </div>
  </section>
</template>

<script>
export default {
  name: "HomeView",
};
</script>
