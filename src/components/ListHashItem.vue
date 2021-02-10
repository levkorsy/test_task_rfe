<template>
    <li class="list-group-item">{{ item }}</li>
</template>

<script>
    export default {
        name: "ListHashItem",
        props:{
            item:{
                type: String,
                required: true
            }
        }
    }
</script>

<style scoped>

</style>