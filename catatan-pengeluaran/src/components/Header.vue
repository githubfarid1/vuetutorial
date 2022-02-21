<template>
    <div>
        <h1>{{ title }}</h1>
    </div>
</template>

<script>
    export default {
        props: {
            title: {
                type: String,
                default: 'te'
            },
        },      
    }
</script>

<style lang="scss" scoped>

</style>