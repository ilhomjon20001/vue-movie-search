<template>
<div class="btn-group">
    <Primirybutton v-for="btn in filterbuttons" 
        :key="btn.name" 
        type="button"
        @click="onfilter(btn.name)" 
        :class="[filterclas == btn.name ? 'btn-dark' : 'btn-outline-dark']"
        >{{btn.title}}</Primirybutton>
</div>
</template>

<script>
import Primirybutton from '../app-uicomponents/Primirybutton.vue';
export default {
    components:{
        Primirybutton,
    },
    data() {
        return {
            filterbuttons:[
                {
                    title:"Barcha kinolar",
                    name:"all",
                    id:1
                },
                {
                    title:"Mashxur kinolar",
                    name:"popular",
                    id:2
                },
                {
                    title:"Eng kop ko'rilgan kinolar",
                    name:"mostviev",
                    id:3
                }
            ],
            filterclas:"all"
        }
    },
    methods: {
        onfilter(item){
            this.filterclas = item
            this.$emit("filtervalu", item)
        }
    },
}
</script>

<style>
.btn-group {
    margin-top: 1rem;
    margin-bottom: 2rem;
}

.btn {
    margin-top: 1.5rem;
}
</style>
