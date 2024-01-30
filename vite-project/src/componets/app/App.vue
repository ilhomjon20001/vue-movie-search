<template>
<div class="app font-monospace">
    <div class="container">
        <Appinfo :allmovie="movies.length" :favouriteMoviesCount='movies.length' />
        <div class="search-panel">
            <SearchPannel />
            <Filter />
        </div>
        <MomMadd :movies="movies" @movionlikeid2="setOnlike" @moviecookie2="setCookie" />
        <AddfilmVue @createMovie="getMovie" />
    </div>
</div>
</template>

<script>
import Appinfo from '../app-info/Appinfo.vue';
import SearchPannel from '../search-panels/SearchPannel.vue';
import Filter from '../app-filter/Filter.vue';
import AddfilmVue from '../app-add/Addfilm.vue';
import MomMadd from '../mom-app-list/MomMadd.vue'
export default {
    components: {
        Appinfo,
        SearchPannel,
        Filter,
        AddfilmVue,
        MomMadd,
    },
    data() {
        return {
            movies: [{
                    name: 'Hazrati Umar',
                    vievers: 455,
                    favourite: false,
                    like: true,
                    id: 1
                },
                {
                    name: 'Ertugrul',
                    vievers: 355,
                    favourite: false,
                    like: true,
                    id: 2
                },
                {
                    name: 'Ottoman Empire',
                    vievers: 255,
                    favourite: true,
                    like: true,
                    id: 3
                }
            ]
        }
    },
    methods: {
        getMovie(item) {
            this.movies.push(item)
        },
        setOnlike(item) {
            this.movies.map(movie => {
                if (movie.id == item) {
                    if (movie.like == true) {
                        movie.like = false
                    } else {
                        movie.like = true
                    }
                }
            })
        },
        setCookie(item) {
            this.movies.map(movie => {
                if (movie.id == item) {
                    if (movie.favourite == true) {
                        movie.favourite = false
                    } else {
                        movie.favourite = true
                    }
                }
            })
        }
    },
}
</script>

<style>
.app {
    height: 100vh;
    color: #000;
}

.content {
    max-width: 1000px;
    background-color: #fff;
    margin: 0 auto;
    padding: 5rem 0;
}

.search-panel {
    margin-top: 1.5rem;
    padding: 1.5rem;
    border-radius: 4px;
    background-color: #fcfaf5;
    box-shadow: 15px 15px 30px rgba(0, 0, 0, 0.15);
}
</style>
