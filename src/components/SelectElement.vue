<template>
    <div class="select text-center">
        <select name="genre" id="genre" @change="$emit('filter_music')" v-model="selectValue">
            <option value="All">Seleziona Genere</option>
            <option v-for="genre in genres" :key="genre.author">{{ genre }}</option>
        </select>
    </div>
</template>

<script>
import axios from 'axios'

export default {
    data() {
        return {
            genres: [],
            selectValue: "All"
        }
    },
    mounted() {
        axios
            .get("https://flynn.boolean.careers/exercises/api/array/music")
            .then(r => {
                this.genres = r.data.response
                this.genres.forEach(genre) => {
                    if () {
                        
                    }
                }
        })
    }
}
</script>

<style lang="scss">
select {
    width: 10%;
    border-radius: 6px;
    background-color: lightgray;
}
</style>