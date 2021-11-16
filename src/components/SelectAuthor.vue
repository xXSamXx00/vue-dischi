<template>
    <select name="author" id="author" @change="$emit('filter_author', selectAuthor)" v-model="selectAuthor">
        <option value="">Seleziona Artista</option>
        <option v-for="author in authors" :key="author.author" :value="author">{{ author }}</option>
    </select>
</template>

<script>
import axios from 'axios'

export default {
    data() {
        return {
            authors: [],
            selectAuthor: ""
        }
    },
    mounted() {
        axios
            .get("https://flynn.boolean.careers/exercises/api/array/music")
            .then(r => {
                r.data.response.forEach((album) => {
                    if (!this.authors.includes(album.author)) {
                        this.authors.push(album.author)
                    }
                });
            }
        );
    }
}
</script>

<style lang="scss">

</style>