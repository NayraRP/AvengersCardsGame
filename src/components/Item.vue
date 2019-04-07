<template>
    <div class="item">
        <div id="main" v-cloak v-on:click="hideTooltip">
            <!-- <div class="tooltip mycard" v-on:click.stop v-if="show_cardtip"> -->
            <div class="tooltip mycard" v-on:click.stop v-if="card.discovered">
                <img class="card" v-on:click.stop="toggleCardtip" :src="getImage(logo)" :alt="card.title">
            </div>
            <!-- <div class="tooltip mycard" v-on:click.stop v-if="!show_cardtip"> -->
            <div class="tooltip mycard" v-on:click.stop v-else>
                <img class="card" v-on:click.stop="toggleCardtip" src="../assets/fondo.png" :alt="card.title">
            </div>
        <!-- <p>{{card.discovered}}</p> -->
        </div>
    </div>
</template>

<script>
import { setTimeout } from 'timers';
    export default {
        name: 'Item',
        props: {
            logo: String,
            index: Number,
            card: Object
        },
        data: function() {
            return {
                show_cardtip: false
            }
        },
        methods: {
            hideTooltip: function() {
                this.show_cardtip = false;
            },
            toggleCardtip: function() {
                console.log("getOpenCard --> " + this.$parent.getOpenCard().num);
                if(this.card.discovered == false) {
                    this.card.discovered = !this.card.discovered;
                    this.$parent.elements[this.index].discovered = true;
                    if(this.card.discovered){
                        console.log("discovered --> true");
                        if (this.$parent.getOpenCard().num == undefined){
                            //asigno carta a auxiliar
                            console.log("num es undefined");
                            this.$parent.setOpenCard(this.card.num, this.index);
                        } else if (this.$parent.getOpenCard().num == this.card.num && this.$parent.getOpenCard().index != this.index) {
                            console.log("iguales..");
                            this.$parent.setCardsDiscover(this.card.num);
                            this.$parent.auxiliar = {};
                        } else {
                            console.log("no iguales...");
                            //poner ambas cartas a discovered false
                            setTimeout(() => {
                                this.$parent.setFalseDiscover(this.card.num);
                                this.$parent.setFalseDiscover(this.$parent.auxiliar.num);
                                this.$parent.auxiliar = {};
                            },1000);
                        }
                    }
                }
            },
            getImage(rute){
                var images = require.context('../assets/', false);
                return images('./'+rute);
            }
        }
    }
</script>

<style scoped>
    [v-cloak]{
        display: none;
    }
    .item {
        width: 120px;
        height: 170px;
        padding: 5%;
        margin: 5%;
    }
    img.card {
        border-radius: 8px;
        width: 120px;
        height: 170px;
        margin: 5%;
        box-shadow: 0 4px 8px 0 rgba(0,0,0,0.4);
        transition: 0.3s;
    }
    img.card:hover {
        box-shadow: 0 4px 8px 0 rgba(0.4,0.4,0.4,0.9);
    }
</style>
