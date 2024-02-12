<template>
<BoxVue >
    <p className='fs-3 text-uppercase'>Barcha kinolar soni: {{ allmovie }}</p>
    <p className='fs-4 text-uppercase'>ko'rilgan kinolar soni:{{ favouriteMoviesCount }}</p>
</BoxVue>
</template>

<script>
import BoxVue from '../app-uicomponents/Box.vue'
export default {
components:{
    BoxVue,
},
props: {
    allmovie: {
        type: Number,
        required: true,
    },
    favouriteMoviesCount: {
        type: Number,
        required: true,
    }
}
}
</script>

<style scoped>
/* .app-info {
    padding: 1.5rem;
    border-radius: 4px;
    background-color: #fcfaf5;
    box-shadow: 15px 15px 30px rgba(0, 0, 0, 0.15);
} */
</style>
