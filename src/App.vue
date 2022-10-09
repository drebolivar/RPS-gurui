<template>
  <div id="app">
    <div class="backgroundImg"/>
           <img src="@/assets/uruchoose.png"/>
    <div class="playingField">
      <div class="flex-row buttons" :key="choice.id" v-for="choice in playerChoices">
    <button class="flex-item" :disabled="playerChoice" :key="choice.id" @click="selectChoice(choice)">
    <img :src="choice.image"/>
    <h4>{{choice.label}}</h4>
    </button>
    </div>
    </div>
    <div class="winner-circle flex-row" v-if="winner">
    <div class="flex-item">
      <h4>Player Choice</h4>
      <img :src="playerChoice.image"/>
    </div>
    <div>{{winner}}
  <div></div><button @click="resetGame()">Another Gamble?</button>
    </div>
    <div class="flex-item">
      <h4>Computer Choice</h4>
      <img :src="compChoice.image" />
    </div>
  </div>
  </div>
</template>

<script>
import choices from './choices.js'

export default {
  name: 'App',
  components: {},
  data: () =>({
    playerChoices: choices,
    playerChoice: null,
    compChoice: null,
    winner: null
  }),
  methods: {
    selectChoice(value){
      this.playerChoice = value

      let compChoiceRandomizer = Math.floor(Math.random() * 3)
      this.compChoice = choices[compChoiceRandomizer]
      this.checkWinner(this.playerChoice, this.compChoice)
    },
    checkWinner(playerChoice, compChoice){
      if (playerChoice === compChoice){
        this.winner = `Draw!`
      } else if (
        (this.playerChoice.id == 1 && this.compChoice.id === 2 || (this.playerChoice.id === 2 && this.compChoice.id === 3) || (this.playerChoice.id === 3 && this.compChoice.id === 1))
      ) {
        this.winner = 'Computer Wins!'
      } else if (
        (this.playerChoice.id === 1 && this.compChoice.id === 3) || (this.playerChoice.id === 2 && this.compChoice.id === 1 ) || (this.playerChoice.id === 3 && this.compChoice.id === 2)) {
          this.winner = 'Player Wins!'
        }
    },
    resetGame(){
      this.playerChoice = null
      this.compChoice = null
      this.winner = null
     }
    }
  }
</script>

<style>
html {
  /* background-color: #383838; */
  background: url('./assets/backgroundgurui.png')
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  align-items: center;
  margin-top: 1px;
  color: #f4f6f9;
}

.flex-row {
  display: flex;
  flex-direction:row;
  justify-content: space-evenly;
  align-items: center;
}

.flex-item {
  padding: 1em;
  max-height: 12em;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  align-items: center;
  background-color: #000000;
  /* background: url('./assets/plaidguri.png'); */
  border-radius: 4px;
  border: 2px solid rgb(255, 107, 107);
  color: #f4f6f9;
  width: 250px;
}

button {
  border: 0;
  cursor: pointer;
  transition: all 0.3s ease;
}

button:disabled {
  cursor: not-allowed;
}

button:hover:not(:disabled) {
  opacity: 0.8;
  border: 1px solid rgba(255, 255, 255, 0.4);
}

.flex-item img {
  width: 250px;
  max-height: 8em;
  align-content: center;
  object-fit: contain;
}

.playingField {
  margin-top: -.5%;
  display: flex;
  flex-direction: row;
  align-items: center;
  justify-content: center;
}

.winner-circle {
  margin-top: .5em;
  border: 1px solid #eaff00;
  border-radius: 4px;
}

.winner-circle button {
  padding: 1em 2em;
  border-radius: 4px;
  border: 0;
  background-color: #ffcc00;
  font-weight: 700;
}

.winner-circle button:hover {
  border: 0;
}
</style>
