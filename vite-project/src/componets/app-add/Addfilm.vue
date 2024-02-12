<template>
<BoxVue class="mt-4">
    <h3>Yangi kino qo'shish</h3>
    <form action="#" class="add-form d-flex" @submit.prevent>
        <input type="text" class="form-control new-post-label" placeholder="Qanday kino?" 
        :value="name"
        @input="name  = $event.target.value"
        >
        <input type="number" class="form-control new-post-label" placeholder="Nechi marotaba ko'rilgan?"
        :value="viwers"
        @input="viwers = $event.target.value"
        >
        <Primirybutton class="btn btn-outline-dark" type="submit"
        v-on:click="addMovie"
        >Qo'shish</Primirybutton>
    </form>
</BoxVue>
</template>

<script>
import Primirybutton from '../app-uicomponents/Primirybutton.vue';
import BoxVue from '../app-uicomponents/Box.vue';
export default {
components:{
    Primirybutton,
    BoxVue
},
data() {
    return {
        name: '',
        viwers:'',
    }
},
methods: {
    addMovie(){
        if(this.name == "" || this.viwers == "") return 
        const newMoviedata = {
            name: this.name,
            vievers: this.viwers,
            favourite: false,
            like: false,
        }
        this.$emit("createMovie", newMoviedata),
        this.name = "",
        this.viwers =""

    }
},
}
</script>

<style>
/* .movies-add-form {
    margin-top: 1.5rem;
    padding: 1.5rem;
    border-radius: 4px;
    background-color: #fcfaf5;
    box-shadow: 15px 15px 30px rgba(0, 0, 0, 0.15);
} */
</style>
