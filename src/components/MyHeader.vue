<template>
  <header>
    <input type="text" v-model="search">
    <button @click="emitSearch">Cerca</button>
  </header>
</template>

<script>

export default {
    name: 'MyHeader',
    data() {
        return {
            search: ''
        }
    },
    methods: {
        emitSearch() {
            this.$emit('search', this.search);
        }
    }
}
</script>

<style>

</style>