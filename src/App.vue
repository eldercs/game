<template>
  <div id="app">
    <div class = "block__buttons">
      <button 
      onclick="document.getElementById('player1').play()" 
      :disabled = "buttonBlock" 
      class = "button-player button-blue" 
      :class="{ blue: this.activeBlue }" 
      @click="compareResult(0)" >0</button>
      <audio id = "player1" src = "./audio/sounds_1.mp3" />

      <button onclick="document.getElementById('player2').play()" 
      :disabled = "buttonBlock" 
      class = "button-player button-red" 
      :class="{ red: this.activeRed }" 
      @click="compareResult(1)">1</button>
      <audio id = "player2" src = "./audio/sounds_2.mp3" />

      <button onclick="document.getElementById('player3').play()" 
      :disabled = "buttonBlock" 
      class = "button-player button-green" 
      :class="{ green: this.activeGreen }" 
      @click="compareResult(2)">2</button>
      <audio id = "player3" src = "./audio/sounds_3.mp3" />

      <button onclick="document.getElementById('player4').play()" 
      :disabled = "buttonBlock" 
      class = "button-player button-yellow" 
      :class="{ yellow: this.activeYellow }" 
      @click="compareResult(3)">3</button>
      <audio id = "player4" src = "./audio/sounds_4.mp3" />
     <!--  <p>{{ round }}</p> -->
    </div>
    <input v-model.number = "difficulty" name="r1" type="radio" value="1500" checked> Легкий
    <input v-model.number = "difficulty" name="r1" type="radio" value="1000"> Средний
    <input v-model.number = "difficulty" name="r1" type="radio" value="400"> Сложный
    <br>
    <button class = "button-start" :disabled = "startBlock" @click="startGame">Start</button>
  </div>
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      difficulty: 1500,
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
      let dif = this.difficulty+250;
      let i = 1;
      item.forEach((item) => {
        if (item == 0) {
          setTimeout(() => {
              (this.activeBlue = true)
              document.getElementById('player1').play()
          }, dif * i);
          setTimeout(() => (this.activeBlue = false), dif * (i + 1) - 250);
          i++;
        } else if (item == 1) {
          setTimeout(() => {
            (this.activeRed = true)
            document.getElementById('player2').play()
          }, dif * i);
          setTimeout(() => (this.activeRed = false), dif * (i + 1) - 250);
          i++;
        } else if (item == 2) {
          setTimeout(() => {
            (this.activeGreen = true)
            document.getElementById('player3').play()
          }, dif * i);
          setTimeout(() => (this.activeGreen = false), dif * (i + 1) - 250);
          i++;
        } else if (item == 3) {
          setTimeout(() => {
            (this.activeYellow = true)
            document.getElementById('player4').play()
          }, dif * i);
          setTimeout(() => (this.activeYellow = false), dif * (i + 1) - 250);
          i++;
        }
      });
      setTimeout(() => ( this.buttonBlock = false), dif * (i));
      setTimeout(() => ( this.startBlock = false), dif * (i));
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
        this.startBlock = false
        this.buttonBlock = true
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
.block__buttons{
  display:grid;
  width:220px;
  gap:10px;
  margin:0 auto;
  grid-template-columns: 100px 100px;
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
.button-player{
  padding:40px;
}
.button-start{
  background: skyblue;
  padding:10px 20px;  
  border-radius: 5px;
  color:black
}
</style>
