<template>
    <div>
        <p>{{ bilangan }}</p>
        <button @click="handler(arg)">clickMe</button>
        <div>
            <p v-if="ganjil">Ganjil</p>
            <p v-if="genap">Genap</p>
            <p>{{ input1 }}</p>
            <input v-model="input1" type="text" />
        </div>
    </div>
</template>

<script>
    export default {
        data(){
            return {
                bilangan: 1,
                input1: '',
                ganjil: false,
                genap: false
            }
        },
        methods: {
            handler() {
                this.bilangan +=1
                if (this.bilangan % 2 == 0) {
                    this.genap = true;
                    this.ganjil = false;
                } else {
                    this.genap = false;
                    this.ganjil = true;

                }
            }
        },
    }
</script>

<style lang="scss" scoped>

</style>
