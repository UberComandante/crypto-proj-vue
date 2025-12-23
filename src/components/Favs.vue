<template>
    <h3>Favorites</h3>

    <div @click="getFromFavs(index)" v-for="(el, index) in massive" :key="index">
        {{ el.from }}
        {{ el.to }}
    </div>
</template>



<script>
    export default {
        data() {

        },
        props: {
            massive: {
                type: Array,
                required: true
            },
            getFromFavs: {
                type: Function,
                required: true 
            }
        }       
    }
</script>


<style scoped>
    h3 {
        display: flex;
        margin: auto;
        justify-content: space-around;
        width: 100px;
        color: blanchedalmond;
    }
    div {
        display: flex;
        margin: auto;
        justify-content: space-around;
        width: 500px;
        margin-top: 10px;
    }
</style>