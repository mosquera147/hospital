<template>
  <div class="home">
    <AppHeader />
    <router-view />
    <div>
      <h2 v-if="turnosDisponibles.length > 0" class="mt-4">
        Turnos Disponibles
      </h2>
      <h2 v-else class="mt-4">Lo sentimos, no hay turnos disponibles</h2>
    </div>
    <div class="row">
      <AppIndex
        v-for="turno in turnosDisponibles"
        :key="turno.name"
        :especialidad="turno.especialidad"
        :fecha="turno.fecha"
        :paciente="turno.user"
        :admin="turno.admin"
        :estado="turno.estado"
        :logueado="'usuario'"
        :id="turno.id"
      />
    </div>
  </div>
</template>

<script>
// @ is an alias to /src
import AppIndex from "@/components/AppIndex.vue";
import AppHeader from "@/components/AppHeader.vue";

export default {
  name: "HomeView",
  data() {
    return {
      turnosDisponibles: [],
    };
  },
  components: {
    AppIndex,
    AppHeader,
  },
  mounted() {
    const url = "https://6655eb763c1d3b60293b98af.mockapi.io/Turnos/?user=null";
    fetch(url, {
      method: "GET",
    })
      .then((res) => res.json())
      .then((data) => {
        data.map((item) => {
          this.turnosDisponibles.push(item);
        });
      })
      .catch((err) =>
        /* eslint-disable */ console.log(...oo_oo(`958059da_0`, err.message))
      );
  },
};
</script>

<style>
html {
  align-items: center;
  width: 100%;
}

.principal {
  background: red;
  height: 90vh;
  background: url("https://static.wixstatic.com/media/7869d1_f010cd7869fa47e88cd9d945642b1dd2~mv2.jpg/v1/fill/w_1000,h_583,al_c,q_90,usm_0.66_1.00_0.01/7869d1_f010cd7869fa47e88cd9d945642b1dd2~mv2.jpg")
    no-repeat center center fixed;
  -webkit-background-size: cover;
  -moz-background-size: cover;
  -o-background-size: cover;
  background-size: cover;
}

.vertical-centered-text {
  -ms-display: flex;
  display: flex;
  /* alineacion vertical */
  align-items: center;
  /* alineacion horizontal */
  justify-content: center;
}
</style>
