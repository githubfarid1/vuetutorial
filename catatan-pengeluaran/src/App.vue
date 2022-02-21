
<template>
  <Header title="Catatan Pengeluaranku"/>
  <FormData @entry-nominal="entryNominal($event)"/>
  <h1>Total Pengeluaran {{ totalPengeluaran }}</h1>
  <h2 v-if="warning">max Pengeluaran reached</h2>

  <ListData v-if="showList" :propPengeluaran="dataPengeluaran"></ListData>
</template>
<script>
  import Header from './components/Header.vue';
  import FormData from './components/FormData.vue';
  import ListData from './components/ListData.vue';
  
  export default {
    components: {
      Header,
      ListData,
      FormData
    },
    data() {
      return {
        dataPengeluaran: [
          // { nominal: 20000, description: 'beli apa'},
          // { nominal: 10000, description: 'beli minum'},
          // { nominal: 30000, description: 'beli makan'},

        ],
        warning: false,
      }
    },
    methods: {
      entryNominal(event) {
        this.dataPengeluaran.push(event)
      }
    },
    computed: {
      showList() {
        return this.dataPengeluaran.length > 0;
      },
      totalPengeluaran() {
        return this.dataPengeluaran.reduce((accum, item) => accum + parseInt(item.nominal), 0);
      }
    },
    watch: {
      //reference totalPengeluaran diatas
      totalPengeluaran: function(val) {
        if (val > 100000) {
          this.warning = true;
        }
      }
    },
  };
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: left;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
