<template>
  <div class="home">
    <ol>
      <li v-for="(i, audio) in audios" :key="i">
        {{audio}}
      </li>
    </ol>
  </div>
</template>

<script lang="ts">
import Vue from 'vue';

export default Vue.extend({
  name: 'Home',
  data: {
    audios: [],
  },
  async created() {
    const response = await fetch(`http://localhost:${process.env.local.BACKEND_PORT}/metrics/audios`);
    let done = false;
    while (!done) {
      const readableStream = await response.body?.getReader().read();
      done = readableStream!.done;
      const value = readableStream?.value;
      this.audios.push(value);
    }
    this.audios = await stream;
    console.log(this.audios);
  }
});
</script>
