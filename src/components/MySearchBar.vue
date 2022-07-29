<template>
    <div>
        <input type="text" placeholder="cerca.." v-model="inputText" @keyup.enter="$emit('search', inputText)">
        <button @click="$emit('search', inputText)">Cerca</button>
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

<style>
</style>