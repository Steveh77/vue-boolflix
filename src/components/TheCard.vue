@<template>
    <ul>
        <li>
            <img :src='getImg' class="movie-poster">
        </li>
        <ul class="description">
            <li><strong>Titolo:</strong> {{ production.title || production.name }}</li>
            <li><strong>Titolo originale:</strong> {{ production.original_title || production.original_name }}</li>
            <li><strong>Voto:</strong> {{ getstars }}</li>
            <li><strong>Lingua: </strong>
                <img v-if="itHadFlags" :src="flagImg" :alt="production.original_language" class="flag">
                <span v-else>{{ production.original_language }}</span>
            </li>
            <li class="overview"><strong>Overview:</strong> {{ production.overview }}</li>
        </ul>
    </ul>
</template>

<script>
export default {
    props: {
        production: Object
    },
    computed: {
        getImg() {
            if (this.production.poster_path == null) {
                return require('../assets/no-video.jpg')
            } else {
                return `https://image.tmdb.org/t/p/w342/${this.production.poster_path}`
            }
        },
        itHadFlags() {
            const flags = ['it', 'en', 'fr', 'ja', 'es']
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

<style lang="scss" scoped>
.flag {
    height: 20px;
}

ul {
    display: flex;
    position: relative;
    flex-direction: column;
    align-items: center;
    list-style-type: none;
    padding: 0;

    .movie-poster {
        width: 342px;
        height: 479px;
        background-color: white;
        object-fit: cover;
    }

    .description {
        position: absolute;
        width: 100%;
        height: 100%;
        cursor: pointer;

        li {
            display: none;
            text-align: center;
            margin: 10px;

        }

        .overview {
            overflow: auto;
        }

    }

    .description:hover {
        background-color: black;
        transition: 0.5s;

        li {
            display: block;
            color: white;
        }
    }

}
</style>