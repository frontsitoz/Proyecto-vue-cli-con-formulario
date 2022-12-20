<template>
  <table :class="mostrar(show)">
    <thead>
      <tr>
        <th>Nombre</th>
        <th>Contraseña</th>
        <th>Correo</th>
        <th>Edad</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td v-for="dato in datos" :key="dato.email">
          {{ dato }}
        </td>
      </tr>
    </tbody>
  </table>
</template>

<script>
export default {
  name: "TablaDatos",
  props: {
    datos: Object,
    show: Boolean,
  },
  methods: {
    mostrar(i) {
      return i ? "s" : "show";
    },
  },
};
</script>

<style scoped>
.show {
  display: none;
}

table{
    margin-top: 25px;
}

td, th {
  border: 1px solid #999;
  padding: 0.5rem;
}
</style>