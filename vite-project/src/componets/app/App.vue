<template>
<div class="app font-monospace">
    <div class="container">
        <Appinfo :allmovie="movies.length" v-bind:favouriteMoviesCount='movies.filter(movie => movie.favourite).length' />
        <BoxVue class="mt-4">
            <SearchPannel @searchmovies="searchfun" />
            <Filter @filtervalu="filtrhandler" />
        </BoxVue>
        <BoxVue class="mt-4 text-center display-3 text-danger" v-if="!movies.length && !isloading">Afsuski filimlar yo'q</BoxVue>
        <BoxVue class="mt-4 text-center display-3 text-dark" v-else-if="isloading">
            <div class="spinner-border" role="status">
                <span class="visually-hidden">Loading...</span>
            </div>
        </BoxVue>
        <MomMadd v-else :movies="filtersearch(onsearch( movies, term),filter)" @movionlikeid2="setOnlike" @moviecookie2="setCookie" @delitecard2="deliteappmovie" />
        <BoxVue>
            <nav aria-label="pagination">
                <ul class="pagination">
                    <li v-for="pagelimit in totalpage" :key="pagelimit" @click="Selectpage(pagelimit)" class="page-item disabled ">
                        <span  class="page-link" :class="[page == pagelimit ? 'text-danger' : 'text-dark']">{{ pagelimit }}</span>
                    </li>
                </ul>
            </nav>
        </BoxVue>
        <AddfilmVue @createMovie="getMovie" />
    </div>
</div>
</template>

<script>
import Appinfo from '../app-info/Appinfo.vue';
import SearchPannel from '../search-panels/SearchPannel.vue';
import Filter from '../app-filter/Filter.vue';
import AddfilmVue from '../app-add/Addfilm.vue';
import MomMadd from '../mom-app-list/MomMadd.vue';
import BoxVue from '../app-uicomponents/Box.vue';
import axios from 'axios'
export default {
    components: {
        Appinfo,
        SearchPannel,
        Filter,
        AddfilmVue,
        MomMadd,
        BoxVue,
        axios,
    },
    data() {
        return {
            movies: [],
            term: "",
            filter: "",
            watchmovies: 0,
            isloading: false,
            totalpage: 0,
            limit: 10,
            page: 1

        }
    },
    methods: {
        async getMovie(item) {
            try {
               const response = await axios.post('https://jsonplaceholder.typicode.com/todos', item) 
            } catch (error) {
                alert(error.message)
            }
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
        },
        async deliteappmovie(item) {
            try {
               const response = await axios.delete(`https://jsonplaceholder.typicode.com/todos/${item}`)
            } catch (error) {
                alert(error.message)
            }
            const movies1 = []
            this.movies.map(movie => {
                if (movie.id !== item) {
                    movies1.push(movie)
                }
            })
            this.movies = movies1
        },
        onsearch(arr, term) {
            if (term.length == 0) {
                return arr
            } else {
                return arr.filter(movie => movie.name.toLowerCase().indexOf(term.toLowerCase()) > -1)
            }
        },
        filtersearch(arr, filter) {
            switch (filter) {
                case 'popular':
                    return arr.filter(movie => movie.like)
                case 'mostviev':
                    return arr.filter(movie => movie.vievers > 300)
                default:
                    return arr
            }
        },
        searchfun(item) {
            this.term = item
        },
        filtrhandler(item) {
            this.filter = item
        },
        Selectpage(page){
            this.page = page
        },
        async getdataonaxios() {
            try {
                this.isloading = true
                const response = await axios.get('https://jsonplaceholder.typicode.com/todos',{
                    params: {
                        _limit: this.limit,
                        _page: this.page
                    }
                })
                    const newarr = response.data.map(item => ({
                        name: item.title,
                        vievers: item.id * 12,
                        favourite: item.completed,
                        like: !item.completed,
                        id: item.id
                    }))
                this.movies = newarr
                this.totalpage = Math.ceil(response.headers['x-total-count'] / this.limit)
            } catch (error) {
                alert("somthing is wrong on server or Your Network")
            } finally {
                this.isloading = false
            }

        }
    },
    mounted() {
        this.getdataonaxios()
    },
    watch:{
        page(){
            this.getdataonaxios()
        }
    }
}
</script>

<style scoped>
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

/* .search-panel {
    margin-top: 1.5rem;
    padding: 1.5rem;
    border-radius: 4px;
    background-color: #fcfaf5;
    box-shadow: 15px 15px 30px rgba(0, 0, 0, 0.15);
} */
</style>
