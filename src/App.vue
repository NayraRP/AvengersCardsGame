<template>
  <div id="app">
    <div id="title">
      <h1>Avengers Cards</h1>
    </div>
    <!-- <item v-cloak v-for="(e,i) in elements" :key="i" :title="e.name" :logo="e.img" :num="e.num" :discovered="e.discovered" :index="i"> -->
    <item v-cloak v-for="(e,i) in elements" :key="i" :title="e.name" :logo="e.img" :num="e.num" :index="i" :card="e">
    </item>

    <div id="my_button">
      <button v-on:click="again">Play Again</button>
    </div>
  </div>
</template>

<script>
import Item from './components/Item.vue'

export default {
  name: 'app',
  components: {
    Item
  },
  data: function() {
    return{
      message: 'You loaded this page on ' + new Date().toLocaleString(),
      auxiliar: {
        type: Object,
        default: ( ()=> {})
      },
      contador: 0,
      elements: [
        {
          "name": "card1",
          "img": "marvel1.png",
          "num": 1,
          "discovered": false
        },
        {
          "name": "card3",
          "img": "marvel3.png",
          "num": 3,
          "discovered": false
        },
        {
          "name": "card2",
          "img": "marvel2.png",
          "num": 2,
          "discovered": false
        },
        {
          "name": "card5",
          "img": "marvel5.png",
          "num": 5,
          "discovered": false
        },
        {
          "name": "card4",
          "img": "marvel4.png",
          "num": 4,
          "discovered": false
        },
        {
          "name": "card6",
          "img": "marvel6.png",
          "num": 6,
          "discovered": false
        },
        {
          "name": "card8",
          "img": "marvel2.png",
          "num": 2,
          "discovered": false
        },
        {
          "name": "card9",
          "img": "marvel3.png",
          "num": 3,
          "discovered": false
        },
        {
          "name": "card7",
          "img": "marvel1.png",
          "num": 1,
          "discovered": false
        },
        {
          "name": "card10",
          "img": "marvel4.png",
          "num": 4,
          "discovered": false
        },
        {
          "name": "card11",
          "img": "marvel5.png",
          "num": 5,
          "discovered": false
        },
        {
          "name": "card12",
          "img": "marvel6.png",
          "num": 6,
          "discovered": false
        }
      ]
    }
  },
  methods:{
    getOpenCard: function() {
      return this.auxiliar;
    },
    setOpenCard: function(num, key){
      this.auxiliar.num = num;
      this.auxiliar.index = key;
      console.log("Auxiliar: " + JSON.stringify(this.auxiliar));
    },
    setCardsDiscover: function(num) {
      this.elements.forEach((element, i) =>  {
        if(element.num == num) {
          this.elements[i].discovered = true;
        }
      })
      console.log("Elements: " + JSON.stringify(this.elements));
    },
    setFalseDiscover: function(num){
      this.elements.forEach((element, i) =>  {
        if(element.num == num) {
          this.elements[i].discovered = false;
        }
      })
      console.log("Elements: " + JSON.stringify(this.elements));
    },
    again: function(){
      console.log("GAME AGAIN!");

      this.elements.forEach((element, i) =>  {
        // if(element.num == num) {
          this.elements[i].discovered = false;
        // }
      })
      //shuffle elements
      this.elements.sort(() => Math.random() -0.5);
      console.log("Elements despues del shuffle: " + JSON.stringify(this.elements));
    }
  }
}
</script>

<style>
  @import url('https://fonts.googleapis.com/css?family=Orbitron');
  :root {
    --textcolor: #fff;
    background: #222;
    font-family: 'Orbitron', sans-serif;
  }
  h1 {
    font-family: 'Orbitron', sans-serif;
  }
  #app {
    font-family: 'Avenir', Helvetica, Arial, sans-serif;
    text-align: center;
    color: #cdd0d2;
    display: grid;
    align-content: center;
    justify-content: center;
    align-items: center;
    /* margin: auto; */
    grid-template-columns: auto auto auto auto auto auto;
    /* width: 30%; */
    /* border: 2px solid #000; */
  }
  button {
    font-family: 'Orbitron', sans-serif;
    font-size: 1.5em;
    background: #222;
    border: none;
    color: #fff;
  }
  button:active{
    color: #2c3e50;
  }
  button:hover{
    text-shadow: 0 4px 8px 0 rgba(0.4,0.4,0.4,0.9);
  }
  #my_button {
    margin-top: 10%;
    margin-bottom: 10%;
    grid-column: 1/7;
  }
  #title {
    margin-top: 1%;
    grid-column: 1/7;
  }
  
</style>
