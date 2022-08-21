<template>
    <div id="searchBar">
        <div class="logo">
            <h1>BOOLFLIX</h1>
        </div>
        <div class="inputSearch">
            <input type="text" placeholder="Cerca.." v-model="inputText" @keyup.enter="$emit('search', inputText)">
            <button @click="$emit('search', inputText)">Cerca</button>
        </div>
    </div>
</template>

<script>
export default {
    data() {
        return {
            inputText: ""
        }
    },
}
</script>

<style lang="scss" scoped>
#searchBar {
    background-color: black;
    height: 70px;
    display: flex;
    justify-content: space-between;

    .logo {
        color: red;

        h1 {
            margin: 18px;
        }
    }

    .inputSearch {
        margin: 25px;

        button {
            background-color: red;
            color: white;
            border: 2px solid red;
        }
    }

}
</style>