<template>
    <ul>
        <li @click="getFunc('BTC')"   :className="perem == 'BTC' ? 'active' : ''">Bitcoin</li>
        <li @click="getFunc('USDT')"  :className="perem == 'USDT' ? 'active' : ''">USDT</li>
        <li @click="getFunc('TRC20')" :className="perem == 'TRC20' ? 'active' : ''">TRC20</li>
        <li @click="getFunc('ERC20')" :className="perem == 'ERC20' ? 'active' : ''">ERC20</li>
        <li @click="getFunc('ETH')"   :className="perem == 'ETH' ? 'active' : ''">Epthirium</li>
    </ul>
</template>


<script>
    export default {
        data() {
            return {
           
            }
        },
        props: {
            getFunc: {
               type: Function,
               required: true
            },
            perem: {
                type: String,
                required: true
            }
        }, 
        methods: {

        }
    }
</script>


<style scoped>
    ul {
        list-style: none;
        width: 200px;
        padding: 0;
        border-radius: 3px;
        border: 3px solid rgb(14, 247, 255);
    }
    li {
        background:  rgb(51, 48, 48);
        color: red;
        padding: 10px 0;
        text-align: center;
    }

    li.active {
        background: greenyellow;
        cursor: pointer;
    }
    
</style>
