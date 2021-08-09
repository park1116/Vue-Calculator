<template>
    <div>
        <button v-on:click="numClick"> {{ num }} </button>
    </div>
</template>

<script>
export default {
    props: ['num'],
    methods: {
        numClick: function() {
            this.$emit('num-click', this.num)
        }
    }
}
</script>

<style>

</style>