@<template>
    <ul>
        <li>{{ production.title || production.name }}</li>
        <li>{{ production.original_title || production.original_name }}</li>
        <li>{{ production.vote_average }}</li>
        <li>
            <img v-if="itHadFlags" :src="flagImg" :alt="production.original_language">
            <span v-else>{{ production.original_language }}</span>
        </li>
    </ul>
</template>

<script>
export default {
    props: {
        production: Object
    },
    computed: {
        itHadFlags() {
            const flags = ['it', 'en']
            return flags.includes(this.production.original_language)
        },
        flagImg() {
            return require(`../assets/flags/${this.production.original_language}.png`)
        }
    },
}
</script>

<style>
img {
    height: 50px;
    width: 70px;
}
</style>