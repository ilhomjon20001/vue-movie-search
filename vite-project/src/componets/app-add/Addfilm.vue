<template>
<div class="movies-add-form">
    <h3>Yangi kino qo'shish</h3>
    <form action="#" class="add-form d-flex" @submit.prevent>
        <input type="text" class="form-control new-post-label" placeholder="Qanday kino?" 
        :value="name"
        @input="name = $event.target.value"
        >
        <input type="number" class="form-control new-post-label" placeholder="Nechi marotaba ko'rilgan?"
        :value="viwers"
        @input="viwers = $event.target.value"
        >
        <button class="btn btn-outline-dark"
        v-on:click="addMovie"
        >Qo'shish</button>
    </form>
</div>
</template>

<script>
export default {
data() {
    return {
        name: '',
        viwers:'',
    }
},
methods: {
    addMovie(){
        const newMoviedata = {
            name: this.name,
            vievers: this.viwers,
            favourite: true,
            like: true,
            id: Date.now()
        }
        this.$emit("createMovie", newMoviedata),
        this.name = "",
        this.viwers =""

    }
},
}
</script>

<style>
.movies-add-form {
    margin-top: 1.5rem;
    padding: 1.5rem;
    border-radius: 4px;
    background-color: #fcfaf5;
    box-shadow: 15px 15px 30px rgba(0, 0, 0, 0.15);
}
</style>
