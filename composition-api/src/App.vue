
<template>
  <div>
    <h1>Luas Segitiga</h1>
    <label for="alas">Alas</label>
    <input v-model="alas" @keyup="hitung" type="number" name="alas">
    <label for="tinggi">Tinggi</label>
    <input v-model="tinggi" @keyup="hitung" type="number" name="tinggi">
    <h3>Luas</h3>
    <h1>{{ luas }}</h1>
  </div>
</template>

<script>
import { ref } from 'vue';
export default {
  name: 'App',
  setup () {
    
    const alas = ref(0);
    const tinggi = ref(0);
    const luas = ref(0);
    function hitung() {
      //console.log('tes');
      luas.value = parseFloat(alas.value) * parseFloat(tinggi.value) * 0.5;
    }

    return {
      alas,
      tinggi,
      luas,
      hitung
    }
  }
}
</script>

<style lang="scss" scoped>

</style>