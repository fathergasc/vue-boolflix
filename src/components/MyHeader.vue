<template>
  <header>
    <span>BOOLFLIX</span>
    <div class="header-right">
        <input type="text" placeholder="Cerca un titolo..." v-model="search" @keyup.enter="emitSearch">
    <button @click="emitSearch" >CERCA</button>
    </div>
    
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
            this.search = '';
        }
    }
}
</script>

<style lang="scss">
 header {
    position: fixed;
    z-index: 999;
    top: 0;
    left: 0;
    width: 100%;
    height: 80px;
    background-color: black;
    display: flex;
    justify-content: space-between;
    align-items: center;

    span {
        color: red;
        font-size: 30px;
        margin-left: 20px;
    }

    .header-right {
        padding-right: 30px;

        input {
            margin : 0 10px;
            padding: 5px;
        }

        button {
            padding: 7px 10px;
            background-color: red;
            border-radius: 8px;
            font-weight: bold;
            color: white;
        }
    }
 }
</style>