<template>
  <div class="home">
    <h1>Welcome to Admin</h1>
    <h3>Your Database visualizer</h3>
    <p>All audios saved: </p>
    <ol>
      <li v-for="(audio, i) in audios" :key="i">
        {{audio}}
      </li>
    </ol>
  </div>
</template>

<script lang="ts">
import Vue from 'vue';
import axios from 'axios';

export default Vue.extend({
  name: 'Home',
  data: () => ({
    audios: [] as Array<string>,
  }),
  async created() {
    const response = await axios.get(`${process.env.VUE_APP_BACKEND_URL}/metrics/audios`);
    this.audios = response.data;
  }
});
</script>
