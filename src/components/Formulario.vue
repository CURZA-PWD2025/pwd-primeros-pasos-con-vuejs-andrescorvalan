<script setup lang="ts">
import { ref } from 'vue'

defineProps<{ msg?: string }>()

const nombre = ref('')
const correo = ref('')
const contrasenia = ref('')
const fechanac = ref('')

function limpiarFormulario() {
  nombre.value = '';
  correo.value = '';
  contrasenia.value = '';
  fechanac.value = '';
}

function crearUsuario() {
  if (nombre.value && correo.value && fechanac.value && contrasenia.value){
    const usuario = {
      nombre: nombre.value,
      correo: correo.value,
      fechanac: fechanac.value,
      contrasenia: contrasenia.value,
      calcularEdad() {
        const ahora = new Date();
        const nacimiento = new Date(fechanac.value);
        let edad = ahora.getFullYear() - nacimiento.getFullYear();
        const mes = ahora.getMonth() - nacimiento.getMonth();
        const dia = ahora.getDate() - nacimiento.getDate();
        if (mes < 0 || (mes === 0 && dia < 0))
          edad--;
        return edad;
      },
      mostrarDatos() {
        alert(
          "Usuario creado correctamente"+
          "\n Nombre: "+this.nombre +
          "\n Correo electronico: "+this.correo +
          "\n Contraseña: "+this.contrasenia +
          "\n Fecha de nacimiento: "+this.fechanac+
          "\n Edad: "+this.calcularEdad());
        limpiarFormulario();
      }
    }
    usuario.mostrarDatos();
  }else 
    alert("Los datos son obligatorios: ");
}
</script>

<template>
  <div class="crear_usuario">
    <h1>{{ msg }}</h1>
    <form class="formulario" @submit.prevent="crearUsuario">

      <label class="labelField">Nombre:
        <abbr title="Ingrese su nombre (obligatorio)">*</abbr>
        <input type="text" v-model="nombre"  placeholder="Debe ingresar su nombre" maxlength="20" pattern="[A-Za-z ]*" required>
      </label>
      <label class="labelField">Correo electr&oacute;nico:
        <abbr title="Ingrese un email (usuario@dominio) (obligatorio)">*</abbr>
        <input type="email" v-model="correo" placeholder="Debe ingresar un email" required>
      </label>
      <label class="labelField">Contraseña:
        <abbr title="Ingrese una contraseña (obligatorio)">*</abbr>
        <input type="password" v-model="contrasenia" placeholder="Ingrese su contraseña" required>
      </label>
      <label class="labelField">Fecha de nacimiento:
        <abbr title="Ingrese su fecha de nacimiento (obligatorio)">*</abbr>
        <input type="date" v-model="fechanac" placeholder="Ingrese su Fecha de Nacimiento" required>
      </label>
      <fieldset>
        <input type="submit" class="boton" value="Crear usuario">
        <input type="reset" class="boton" value="Limpiar formulario" @click="limpiarFormulario">
      </fieldset>
    </form>
    <div class="datosFormulario"> 
      <h2>Datos ingresados</h2>
      <p>Nombre: {{ nombre }}</p>
      <p>Contraseña: {{ contrasenia }}</p>
      <p>Correo electronico: {{ correo }}</p>
      <p>Fecha de nacimiento: {{ fechanac }}</p>
    </div>
  </div>
</template>

<style scoped>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
} 
.crear_usuario {
  margin:0.5em;
  background-color:gainsboro;
  border-radius: 0.5em 0.5em 0.5em 0.5em;
  border: 1px solid blue;
  text-align: center;
}
.formulario {
  background-color:gainsboro;
  border-radius: 0.5em 0.5em 0.5em 0.5em;
  border: 1px solid blue;
  margin: 0.5em;
  text-align: left;
}
fieldset {
  border:0;
  margin: 0.5em;
  text-align: center;
}
.labelField {
  display: block;
  margin: 0.5em;
}
.labelField abbr {
  display: inline-block;
  color: red;
  text-decoration: none;
}
input {
  border-radius: 0.5em 0.5em 0.5em 0.5em;
  border: 1px solid green;
  width: 100%;
  height:2em;
}
.boton{
  border-radius: 0.5em 0.5em 0.5em 0.5em;
  border: 1px solid blue;
  display: inline-block;
  margin: 0.5em;
  padding: 0.2em 0.4em 0.2em 0.4em;
  text-align: right;
  width: auto;
  font-size: 1em;
}
.datosFormulario {
  border-radius: 0.5em 0.5em 0.5em 0.5em;
  border: 1px solid green;
  margin: 0.5em;
  background-color:lightblue;
}
</style>
