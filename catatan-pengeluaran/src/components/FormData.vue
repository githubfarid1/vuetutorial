<template>
    <div>
        <form class="form-pengeluaran" @submit.prevent="catat">
            <div>
                <label for="">Pengeluaran</label>
                <input v-model="nominal" type="number" id="nominal">
            </div>
            <div>
                <label for="">Keterangan</label>
                <input v-model="keterangan" type="text" id="keterangan">
            </div>
            <div>
                <button>Submit</button>
            </div>

        </form>
    </div>
</template>

<script>
    export default {
        data() {
            return {
                nominal: null,
                keterangan: null,
            }
        },
        methods: {
            catat() {
                this.$emit('entry-nominal', {
                    nominal: this.nominal,
                    description: this.keterangan,
                });
                this.nominal = null;
                this.keterangan = null;
                document.getElementById('nominal').focus();
            }   
        },
    }
</script>

<style lang="scss" scoped>

</style>