<template>
    <main class="px-3 py-5">
        <MusicList/>
    </main>
</template>

<script>
import MusicList from './MusicList.vue'

export default {
    components: {
        MusicList
    }
}
</script>

<style lang="scss">
main {
    background-color: #1e2d3b;
}
</style>