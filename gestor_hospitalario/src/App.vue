<template>
  <div id="app">
    <router-view />
  </div>
</template>

<script>
import store from "./store/store.js";

export default {
  data() {
    return {
      especialidades: [],
      estados: [],
      turnos: [],
      usuarios: [],
    };
  },

  async created() {
    const respuesta = await fetch(
      "https://66589c1f5c36170526493211.mockapi.io/Especialidades"
    );
    this.especialidades = await respuesta.json();
    const estados = await fetch(
      "https://66589c1f5c36170526493211.mockapi.io/Estado"
    );
    this.estados = await estados.json();
    const turnos = await fetch(
      "https://6655eb763c1d3b60293b98af.mockapi.io/Turnos"
    );
    this.turnos = await turnos.json();
    const usuarios = await fetch(
      "https://6655eb763c1d3b60293b98af.mockapi.io/Usuarios"
    );
    this.usuarios = await usuarios.json();
    store.dispatch("addEspecialidades", this.especialidades);
    store.dispatch("addEstados", this.estados);
    store.dispatch("addTurnos", this.turnos);
    store.dispatch("addUsuarios", this.usuarios);
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

html {
  width: 100px;
  margin: auto;
}

nav {
  padding: 30px;
}

nav a {
  font-weight: bold;
  color: #2c3e50;
}

nav a.router-link-exact-active {
  color: #42b983;
}
</style>
