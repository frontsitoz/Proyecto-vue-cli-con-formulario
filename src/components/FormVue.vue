<template>
  <div class="container">
    <form action="" @submit.prevent="contacto">
      <label for="nombre">Nombre</label>
      <input
        v-model="nombre"
        type="text"
        required
        id="nombre"
        placeholder="Ingresar nombre"
      />
      <p v-if="nombre && nameValidation">
        El nombre debe tener al menos 6 caracteres.
      </p>

      <label for="email">Correo</label>
      <input
        v-model="email"
        type="email"
        required
        id="email"
        placeholder="Ingresar correo"
      />
      <p v-if="email && !emailValidation">Correo inválido</p>

      <label for="contra">Contraseña</label>
      <input
        v-model="contra"
        type="password"
        required
        id="contra"
        placeholder="Ingresar contraseña"
      />
      <p v-if="contra && passwordLength">
        La contraseña debe tener al menos 6 caracteres.
      </p>

      <label for="edad">Edad</label>
      <input
        v-model="edad"
        type="number"
        required
        id="edad"
        placeholder="Ingresar edad"
      />
      <p v-if="!edadValidation && edad">Edad inválida</p>
      <p>
        {{ edad }}
      </p>

      <input type="submit" value="Enviar" />
    </form>
    <tabla-datos :show="mostrarTabla" :datos="datos"></tabla-datos>
  </div>
</template>

<script>
import TablaDatos from "./TablaDatos.vue";

export default {
  name: "FormVue",
  components: {
    TablaDatos,
  },
  data() {
    return {
      nombre: "",
      contra: "",
      email: "",
      edad: "",
      mostrarTabla: false,
      datos: {
        nombre: "",
        contra: "",
        email: "",
        edad: 0,
      },
      error: 0,
    };
  },
  methods: {
    contacto() {
      this.error = 0;
      this.passwordLength ? this.error++ : (this.datos.contra = this.contra);
      this.emailValidation ? (this.datos.email = this.email) : this.error++;
      this.edadValidation ? (this.datos.edad = this.edad) : this.error++;
      this.nameValidation ? this.error++ : (this.datos.nombre = this.nombre);
      if (this.error > 0) {
          this.mostrarTabla = false;
      } else {
          this.mostrarTabla = true;
      }
    },
  },
  computed: {
    passwordLength() {
      if (this.contra != null) return this.contra.length < 6;
      return false;
    },
    emailValidation() {
      return /^(([^<>()[\]\\.,;:\s@"]+(\.[^<>()[\]\\.,;:\s@"]+)*)|(".+"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,}))$/.test(
        this.email.toLowerCase()
      );
    },
    edadValidation() {
      return /^[0-9]*$/gm.test(this.edad);
    },
    nameValidation() {
      if (this.nombre != null) return this.nombre.length < 6;
      return false;
    },
  },
};
</script>

<style scoped>
form {
  display: flex;
  flex-direction: column;
}

.container {
  margin: auto;
  max-width: 800px;
}
</style>