<template>
    <div>
        <table>
            <tr>
                <th>Pengeluaran</th>
                <th>Keterangan</th>
            </tr>
            <tr v-for="(pengeluaran, index) in propPengeluaran" :key="index">
                <td>{{ pengeluaran.nominal }}</td>
                <td>{{ pengeluaran.description }}</td>
            </tr>
        </table>
    </div>
</template>

<script>
    export default {
        props: {
            propPengeluaran: {
                type: Array,
            },
        },
    }
</script>

<style scoped>
    table {
        border-collapse: collapse;
        width: 100%;
    }
    table, th, td{
        border: 1px solid black;
    }
    th {
        background-color:aqua;
    }
</style>