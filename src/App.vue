<template>

    <div className="mains">
        <h1>Crypto traider</h1>
        <input min="0" type="number" id="inp" @input="userData($event.target.value)">
        <button id="but1" @click="convert()">Convert</button>
        <button @click="addFav()" id="but2">Добавить в избранное</button>
        {{ number }}
        {{ perem1 }}
        {{ perem2 }}
        <br>
        {{ errorMes }}
        {{ result }}
        
    </div>

    <div className="selectors">
        <Selector :getFunc="getPerem1"  :perem="perem1"/>
        <Selector :getFunc="getPerem2" :perem="perem2"/>
    </div>

    <div>
        <Favs :massive="favorites" v-if="favorites.length > 0" :getFromFavs="getFromFavs" />
    </div>

</template>



<script>
    import Selector from './components/Selector.vue';
    import CryptoConvert from 'crypto-convert';
    import Favs from './components/Favs.vue'; 


    const convert = new CryptoConvert();

    export default {
        components: { Selector, Favs },
        data() {
            return {
                number: null,
                perem1: "",
                perem2: "",
                errorMes: "",
                result: "",
                favorites: []
            }
        },
        methods: {
            userData(val) {
                this.number = val;
            },
             getPerem1(val) {
                 this.perem1 = val
             },
             getPerem2(val) {
                 this.perem2 = val
             },
            async convert() {
                if(this.number <= 0) {
                    this.errorMes = "Введите число больше нуля";
                    this.result = null;
                    return
                } else if(this.perem1 == "" || this.perem2 == "") {
                    this.errorMes = "Выберите валюту"
                    this.result = null;
                    return
                } else if(this.perem1 == this.perem2) {
                    this.errorMes = "Нельзя конвертировать само в себя";
                    this.result = null;
                    return
                } else {
                    this.errorMes = ""
                }

                await convert.ready();
                
                if(this.perem1 == "BTC" && this.perem2 == "USDT") {
                    this.result = convert.BTC.USDT(this.number);
                } else if(this.perem1 == 'BTC' && this.perem2 == 'TRC20') {
                    this.result = convert.BTC.TRC20(this.number);
                } else if(this.perem1 == 'BTC' && this.perem2 == 'ERC20') {
                    this.result = convert.BTC.ERC20(this.number);
                } else if(this.perem1 == 'BTC' && this.perem2 == 'ETH') {
                    this.result = convert.BTC.ETH(this.number);
                } 
                
                else if(this.perem1 == 'USDT' && this.perem2 == 'BTC') {
                    this.result = convert.USDT.BTC(this.number);
                } 
                // и т.д. else if для всех позиций
                

            },
            addFav() {
                this.favorites.push({
                    from: this.perem1,
                    to: this.perem2
                })
            },
            getFromFavs(index) {
                this.perem1 = this.favorites[index].from
                this.perem2 = this.favorites[index].to
            }
        }
    }
</script>


<style scoped>
    input {
        outline: none;
        border-radius: 5px;
        width: 200px;
        height: 20px;
        top: -30px;
    }

    .selectors {
        display: flex;
        justify-content: space-around;

        width: 600px;
        margin: auto;
    }

    #but1 {
        background-color: goldenrod;
        height: 25px;
        border-radius: 3px;
    }
     #but2 {
        background-color: goldenrod;
        height: 25px;
        border-radius: 3px;
    }
</style>
