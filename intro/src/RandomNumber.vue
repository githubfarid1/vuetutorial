<template>
    <div>
        <h1>Conditional</h1>
        <p>{{ number }}</p>
        <h4 v-if="even">Genap</h4>
        <h4 v-if="odd">Ganjil</h4>
        <button @click="generate(arg)">Generate</button>
    </div>
</template>

<script>
    export default {
        data() {
            return {
                number: 0,
                even: false,
                odd: false
            }
        },
        mounted () {
            this.generate();
        },
        methods: {
            generate() {
                this.number = Math.floor(Math.random() * 100);
                this.evaluate();
            },
            evaluate() {
                if (this.number % 2 == 0) {
                    this.even = true;
                    this.odd = false;
                } else {
                    this.even = false;
                    this.odd = true;
                }
            }
        },
    }
</script>

<style lang="scss" scoped>

</style>