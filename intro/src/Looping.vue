<template>
    <div>
        <h1>Looping</h1>
        <ol>
            <li v-for="day in days" v-bind:key="day">
                {{ day }}
            </li>
        </ol>
        <table>
            <tr v-for="day in days" v-bind:key="day">
                <td>{{ day }}</td>
            </tr>
        </table>
    </div>
</template>

<script>
    export default {
        data() {
            return {
                days: ['Ahad', 'Senin', 'Selasa', 'Rabu', 'Kamis', 'Jumat', 'Sabtu']
            }
        },
    }
</script>

<style lang="scss" scoped>

</style>