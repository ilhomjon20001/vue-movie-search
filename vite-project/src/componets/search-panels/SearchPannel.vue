<template>
<form action="#">
    <input type="text" class="form-control search-input " placeholder="kinolarni qidrish" 
    v-bind:value="moviname"
    @input="moviname = $event.target.value"
    v-on:input="searchmovie">
</form>
</template>

<script>
export default {
    data() {
        return {
            moviname:""
        }
    },
    methods: {
        searchmovie(){
            const movinames = this.moviname
            this.$emit("searchmovies", movinames)
        }
    },
}
</script>

// <style scoped>
.search-input {
    padding: 1.5rem;
    border-radius: 4px;
    background-color: #fcfaf5;
    box-shadow: 15px 15px 30px rgba(0, 0, 0, 0.15);
}
</style>
