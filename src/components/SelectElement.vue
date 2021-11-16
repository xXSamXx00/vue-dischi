<template>
    <div class="select text-center">
        <select name="genre" id="genre" @change="$emit('filter_music')">
            <option value="Rock">Rock</option>
            <option value="Pop">Pop</option>
            <option value="Jazz">Jazz</option>
            <option value="Metal">Metal</option>
        </select>
    </div>
</template>

<script>
export default {

}
</script>

<style lang="scss">
select {
    width: 10%;
    border-radius: 6px;
    background-color: lightgray;
}
</style>