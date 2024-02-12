<template>
<BoxVue>
    <Movielist v-for="movie in movies" 
     v-bind:movie="movie" :key="movie.id"
     @movionlikeid="this.$emit('movionlikeid2', movie.id)"
     @moviecookie="this.$emit('moviecookie2',  movie.id)"
     @delitecard="this.$emit('delitecard2',  movie.id)"/>
</BoxVue>
</template>

<script>
import Movielist from '../app-list/Movielist.vue';
import BoxVue from '../app-uicomponents/Box.vue';
export default {
    components: {
        Movielist,
        BoxVue,
    },
    props: {
        movies: {
            type: Array,
            required: true,
        }
    }
}
</script>

<style scoped>
/* .movie-list {
    padding: 1.5rem;
    border-radius: 4px;
    background-color: #fcfaf5;
    box-shadow: 15px 15px 30px rgba(0, 0, 0, 0.15);
} */
</style>
