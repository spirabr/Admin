<template>
  <div class="home">
    <header>
      <h1>Admin Spira</h1>
      <h3>Interface para o Banco de Dados Spira</h3>
    </header>

    <body>
      <div class="grid">
        <p class="index"> index </p>
        <p class="audios"> audios </p>
        <p class="timestamps"> timestamps </p>
      </div>
      <div :class="(i-1) % 8 < 4 ? 'grid' : 'grid alt-color'" v-for="i in audios.length" :key="i">
        <p class="index"> {{i}} </p>
        <p class="audios"> {{audios[i - 1]}} </p>
        <p class="timestamps"> {{timestamps[i - 1]}} </p>
      </div>
    </body>
  </div>
</template>

<script lang="ts">
import Vue from 'vue';
import axios from 'axios';

export default Vue.extend({
  name: 'Home',
  data: () => ({
    audios: [] as Array<string>,
    timestamps: [] as Array<string>,
  }),
  async created() {
    const response = await axios.get(`${process.env.VUE_APP_BACKEND_URL}/metrics/audios`);
    this.audios = response.data.sort().map((audio : string) => audio.substring(23).replaceAll('_', ' '))
    this.timestamps = response.data.sort().map((timestamp : string) => timestamp.substring(0, 23).replace('_', ' '));
  }
});
</script>

<style scoped>
  .home {
    align-items: center;
    padding: 1rem 2rem;
  }
  header h1 {
    color: #7c31f4;;
  }
  body .grid {
    padding: 1rem;

    display: grid;
    grid-template-columns: [index] 1fr [audios] 8fr [timestamps] 8fr;
    grid-template-rows: auto;

    border: 1px solid black;
  }
  .index {
    grid-column: 1fr;
  }
  .audios {
    grid-column: 1fr;
  }
  .timestamps {
    grid-column: 1fr;
  }
  .alt-color {
    background-color: lightgrey;
  }
</style>