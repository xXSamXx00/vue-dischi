<template>
    <select name="genre" id="genre" @change="$emit('filter_gen', selectGen)" v-model="selectGen" class="me-5">
        <option value="">Seleziona Genere</option>
        <option v-for="genre in genres" :key="genre.genre" :value="genre">{{ genre }}</option>
    </select>
</template>

<script>
import axios from 'axios'

export default {
    data() {
        return {
            genres: [],
            selectGen: ""
        }
    },
    mounted() {
        axios
            .get("https://flynn.boolean.careers/exercises/api/array/music")
            .then(r => {
                r.data.response.forEach((album) => {
                    if (!this.genres.includes(album.genre)) {
                        this.genres.push(album.genre)
                    }
                });
            }
        );
    },
    methods: {

    }
}
</script>

<style lang="scss">

</style>