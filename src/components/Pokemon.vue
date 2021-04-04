<template>
    <h1> {{ num }} {{ upper(name) }} </h1>
    <small> {{ url }} </small>

</template>

<script>
export default {
    props: {
        num: Number,
        name: String,
        url: String
    },
    methods: {
        upper: function(value){
            const newName = value[0].toUpperCase() + value.slice(1);
            return newName;
        }
    }
}
</script>


<style>

</style>