<template>
  <div id="app">
    <div>
      <button :disabled = "buttonBlock" class = "button-blue" :class="{ blue: this.activeBlue }" @click="compareResult(0)">0</button>
      <button :disabled = "buttonBlock" class = "button-red" :class="{ red: this.activeRed }" @click="compareResult(1)">1</button>
      <button :disabled = "buttonBlock" class = "button-green" :class="{ green: this.activeGreen }" @click="compareResult(2)">2</button>
      <button :disabled = "buttonBlock" class = "button-yellow" :class="{ yellow: this.activeYellow }" @click="compareResult(3)">3</button>
     <!--  <p>{{ round }}</p> -->
    </div>
    <button :disabled = "startBlock" @click="startGame">Start</button>
  </div>
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      buttonBlock: true,
      startBlock: false,
      round: [],
      complateRound: [],
      activeBlue: false,
      activeRed: false,
      activeGreen: false,
      activeYellow: false,
    };
  },
  methods: {
    startGame() {
      this.round = [] 
      this.buttonBlock = true;
      this.startBlock = true
      this.round.push(Math.floor(Math.random() * 4));
      this.combinationColor(this.round);
    },
    combinationColor(item) {
      this.buttonBlock = true;
      this.startBlock = true
      let i = 1;
      item.forEach((item) => {
        if (item == 0) {
          setTimeout(() => (this.activeBlue = true), 1500 * i);
          setTimeout(() => (this.activeBlue = false), 1400 * (i + 1));
          i++;
        } else if (item == 1) {
          setTimeout(() => (this.activeRed = true), 1500 * i);
          setTimeout(() => (this.activeRed = false), 1400 * (i + 1));
          i++;
        } else if (item == 2) {
          setTimeout(() => (this.activeGreen = true), 1500 * i);
          setTimeout(() => (this.activeGreen = false), 1400 * (i + 1));
          i++;
        } else if (item == 3) {
          setTimeout(() => (this.activeYellow = true), 1500 * i);
          setTimeout(() => (this.activeYellow = false), 1400 * (i + 1));
          i++;
        }
      });
      setTimeout(() => ( this.buttonBlock = false), 1400 * (i));
      setTimeout(() => ( this.startBlock = false), 1400 * (i));
    },
    compareResult(idButton){
      this.complateRound.push(idButton);
      console.log(this.complateRound[this.complateRound.length-1])
      if(this.complateRound[this.complateRound.length-1] === this.round[this.complateRound.length-1]){
        if(this.complateRound.length === this.round.length){
           this.complateRound = []
           this.round.push(Math.floor(Math.random() * 4));
           this.combinationColor(this.round);
        }
      }
      else{
        console.log("nooo:", this.round[this.complateRound.length-1])
        this.complateRound = []
        this.round = [] 
        this.startBlock = false;
      }
    }
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
.blue {
  background: blue;
}
.button-blue:active {
  background: blue;
}
.red {
  background: red;
}
.button-red:active{
  background: red;
}
.green {
  background: green;
}
.button-green:active{
  background: green;
}
.yellow {
  background: yellow;
}
.button-yellow:active{
  background: yellow;
}
button{
  padding:10px;
}
</style>
