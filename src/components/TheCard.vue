@<template>
    <ul>
        <li>
            <img :src='getImg'>
        </li>
        <li>{{ production.title || production.name }}</li>
        <li>{{ production.original_title || production.original_name }}</li>
        <li>{{ getstars }}</li>
        <li>
            <img v-if="itHadFlags" :src="flagImg" :alt="production.original_language" class="flag">
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
        getImg() {
            return `https://image.tmdb.org/t/p/w342/${this.production.poster_path}`
        },
        itHadFlags() {
            const flags = ['it', 'en']
            return flags.includes(this.production.original_language)
        },
        flagImg() {
            return require(`../assets/flags/${this.production.original_language}.png`)
        },
        getstars() {
            let valutation = Math.ceil(this.production.vote_average / 2)
            let starValutation = ""
            if (valutation === 0) {
                starValutation = "Non valutato"
            } else {
                for (let i = 0; i < valutation; i++) {
                    starValutation += '⭐';
                }
            }
            return starValutation
        }
    },
}
</script>

<style>
.flag {
    height: 50px;
    width: 70px;
}

ul {
    border: 1px solid black;
    display: flex;
    flex-direction: column;
    align-items: center;
    list-style-type: none;
    padding: 0;
}
</style>