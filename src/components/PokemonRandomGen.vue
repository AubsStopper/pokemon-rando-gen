<template>
 <div>
    <div id="main" >
      <div class="name"> {{ nameDisplay }} </div>
        <transition name="slide-fade">
          <div id="pokeball-container" v-show="!show" >
            <img id="pokeball" src="https://pngimg.com/uploads/pokeball/pokeball_PNG21.png" :style="{ height: window.height + 'px' }" >
          </div>
        </transition>
        <transition name= "fade">  
          <div id="pokemon-container" v-show="show">  
            <img id="pokemon"  v-show='show'  v-bind:src="char1" :style="{ height: window.height + 'px', width: window.width }">
          </div>
        </transition>
      <div class="button-container">
        <button v-on:click='toggle' v-if="!show">Toss The Ball</button>   
        <button v-on:click='toggle' v-else>Get Another Ball</button>   
        <MoreInfoModal v-show="false" :wholechar="wholechar"/>
      </div>
      </div>
   </div>
</template>

<script>
import axios from "axios";
import MoreInfoModal from './MoreInfoModal.vue'


export default {
  name: 'Body',
  components: {
    MoreInfoModal
  },
  data() {
    return {
      characters: null,
      charName: null,
      wholechar: {},
      charURL: null,
      charURLID: null,
      nameDisplay:"",
      char1: null,
      window: {
        width: 0,
        height: 0
      },
      IdCollection: [],
      max: 898,
      show: false,
      officalartwork: "offical-artwork",
      id: 6,
      randCharID: null,
      tempChar: "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/dream-world/132.svg"
    }
  },
  props: {
    msg: String
  },
  created() {
    window.addEventListener('resize', this.handleResize);
    this.handleResize();
    this.getAllCharacters();
  },
  mounted() {
  },
  unmounted() {
    window.removeEventListener('resize', this.handleResize);
  },
  methods: {
    handleResize() {
      this.window.width = window.innerWidth - 200;
      this.window.height = window.innerHeight - 221;

      console.log(window.innerWidth)
      console.log(window.innerHeight)

      if (this.window.width < this.window.height) {
          this.window.height = window.innerWidth - 221;
      } else {
          this.window.width = window.innerHeight - 200;
      }      
      console.log("Height " + window.width);
      console.log("Width " + window.height);
    },
    nameDisplaymethod() {
      setTimeout(() => {
          this.nameDisplay = this.charName
      }, 500)
    },
    getAllCharacters: function () {
      axios
        .get('https://pokeapi.co/api/v2/pokemon/?limit=2000')
        .then((response) => {
          this.characters = response.data;  

          let idArray = []
          for (var i = 0; i < response.data.count; i++) {
                Object.values(this.characters.results).forEach(value => {
               //idArray.push(value.url.substring(34).replace("/",""))
                idArray.push(value.name)
                })
                this.IdCollection = idArray
            }
        }).catch(err => {
          console.log(err)
        })
    },
    getOneCharacter: function (id) {
      axios
        .get(`https://pokeapi.co/api/v2/pokemon/${id}`)
        .then((response) => {
          this.wholechar = response.data;
          this.char1 = response.data.sprites.other.dream_world.front_default;
          
          if (!response.data.sprites.other.dream_world.front_default) {
            // Temp Fix until we can cascade another image
            console.log("try again")
            this.getOneCharacter(this.IdCollection[this.getRandInt()])
          }
          this.charName = response.data.name;
          this.nameDisplaymethod()

          }).catch(err => {
            console.log("That's a bad", err)
          })
    },
    getRandInt: function() {
      return Math.floor(Math.random() * this.IdCollection.length); 
   },
  toggle() {
    this.show = !this.show
    if (this.show) {
      setTimeout(() => {
        this.getOneCharacter(this.IdCollection[this.getRandInt()])
      }, 1500 );
    } else {
      this.charName = null;
      this.char1 = null;
      this.nameDisplay = "";
    }
  },
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style>

.name {
  font-weight: 700;
  font-size: 30px;
  margin-bottom: 10px;
  height: 30px;
}

#main {
  margin-top: 100px;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  align-content: space-between;
  height: 80vh;
}

h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}

#pokeball-container {
  display: flex;
  justify-content: center;
  align-items: center;
}

#pokemon-container {
  display: flex;
  justify-content: center;
  align-items: center;
}

.button-container {
  display: flex;
  justify-content: space-between;
    margin: 20px;
}

.slide-fade-enter-active {
  transition: all 6s ease;
}
.slide-fade-leave-active {
  transition: all 1.5s cubic-bezier(1.0, 0.5, 0.8, 1.0);
 
}
.slide-fade-enter, .slide-fade-leave-to
/* .slide-fade-leave-active below version 2.1.8 */ {
  opacity: 0;
   transform: scale(.1);
  animation: bounce-in .8s; 
}

@keyframes bounce-in {
  from, to { transform: scale(1, 0); }
  0% {
    transform: scale(0.9, 1.1)
  }
  25% {
    transform: scale(.8);
    transform: translateX(10px)
  }
  50%{
      transform: scale(.5);
      transform: translateX(10px)
  }
  75% {
      transform: scale(.4);
      transform: translateX(10px)
  }
  100% {
    transform: scale(.1);
  }
}

.fade-enter,
.fade-leave-to {
  opacity: 0;
}

.fade-enter-active,
.fade-leave-active {
  transition: 0.5s;
}

button {
	box-shadow: 3px 4px 0px 0px #1564ad;
	background:linear-gradient(to bottom, #79bbff 5%, #378de5 100%);
	background-color:#79bbff;
	border-radius:5px;
	border:1px solid #337bc4;
	display:inline-block;
	cursor:pointer;
	color:#ffffff;
	font-family:Arial;
	font-size:17px;
	font-weight:bold;
	padding:12px 44px;
	text-decoration:none;
	text-shadow:0px 1px 0px #528ecc;
}
.button:hover {
	background:linear-gradient(to bottom, #378de5 5%, #79bbff 100%);
	background-color:#378de5;
}
.button:active {
	position:relative;
	top:1px;
}

@media only screen and (max-width: 600px) {
  #main {
    margin-top: 150px;
  }
}

</style>
