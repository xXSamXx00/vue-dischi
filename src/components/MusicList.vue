<template>
    <div class="cards_music">
        <div class="select text-center d-flex justify-content-center">
            <SelectGenre :selectGen="searchValue" @filter_gen="searchMusic"/>
            <SelectAuthor :selectAuthor="selectAuthor" @filter_author="searchAuthor"/>
        </div>
        <div class="row gx-5 my-5 justify-content-center" v-if="!loading">
            <div class="col-md-2 text-center card_music my-3" v-for="music in filterMusics" :key="music.title">
                <div class="content p-4">
                    <img :src="music.poster" :alt="music.author" class="img-fluid">
                    <h2 class="title mt-3">{{ music.title }}</h2>
                    <p class="text mt-4">{{ music.author }}<br>{{ music.year }}</p>
                </div>
            </div>
        </div>
        <div v-else>
            <h2 class="loading text-center mt-5">Caricamento...</h2>
        </div>
    </div>
</template>

<script>
import SelectGenre from './SelectGenre.vue'
import SelectAuthor from './SelectAuthor.vue'
import axios from 'axios'

export default {
    components: {
        SelectGenre,
        SelectAuthor
    },
    data() {
        return {
            musics: [],
            loading: true,
            API_URL: "https://flynn.boolean.careers/exercises/api/array/music",
            searchValue: "",
            selectAuthor: ""
        }
    },
    mounted() {
        setTimeout(this.callApi, 1000)
    },
    methods: {
        callApi() {
            axios
                .get(this.API_URL)
                .then(r => {
                    console.log(r);
                    this.musics = r.data.response
                    this.loading = false
            }).catch(e => {
                console.log(e, "ERROR!");
            })
        },
        searchMusic(value) {
            this.searchValue = value
        },
        searchAuthor(author) {
            this.selectAuthor = author
        }
    },
    computed: {
        filterMusics() {
            if (this.searchValue === "" && this.selectAuthor === "") {
                return this.musics;
            } else {
                let filterMusic = this.musics.filter((music) => {
                    return (music.genre.includes(this.searchValue) && music.author.includes(this.selectAuthor));
                })
                return filterMusic
            }
        }
    }
}
</script>

<style lang="scss">
.row {
    margin: 0 !important;
    .content {
        background-color: #2e3a46;
        height: 450px;
        .title {
            color: white;
            text-transform: uppercase;
            font-size: 25px;
            padding: 0 25px;
        }
        .text {
            color: #758080;
            font-size: 20px;
        }
    }
}
.loading {
    color: white;
}
select {
    width: 10%;
    border-radius: 6px;
    background-color: lightgray;
}
</style>