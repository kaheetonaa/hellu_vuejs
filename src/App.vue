<template>
  <h1>{{ msg }}</h1>
  <input v-model="msg"><br /><br />

  <button @click="handler">click me</button>
  <p>{{ output }}</p>
  <svg :id="drawing"></svg>
</template>
<script>
import axios from 'axios';

const ENDPOINT = 'https://nominatim.openstreetmap.org/search';
const FORMAT = 'json';

export default {
  data() {
    return {
      msg: 'Milano',
      output: ''
    }
  },
  methods: {
    async handler(event) {
      if (event) {

        let result=await axios.get(ENDPOINT, {
          params: {
            q: this.msg,
            format: FORMAT,
            limit: 1,
            polygon_svg: 1
          }
        })
        this.output=result.data[0].svg
      }
    }
  }
}
</script>

<style>

</style>