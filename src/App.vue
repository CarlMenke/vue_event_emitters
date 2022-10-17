<template>
  <div id="app">
    <div class="flex-row buttons">
      <button class="flex-item" v-for="choice in playerChoices" :key="choice.id" :disabled="playerChoice" @click="selectChoice(choice)">
        <img v-bind:src = 'choice.image' v-bind:alt = 'choice.label'/>
        <h4>{{choice.label}}</h4>
      </button>
    </div>
    <button class="flex-item" @click="resetGame()">Reset</button>
    <div class="winner-circle flex-row" v-if="winner">
      {{winner}}
      <div class="flex-item " v-if="winner">
        Player:
        <img v-bind:src = 'playerChoice.image' v-bind:alt = 'playerChoice.label'/>
        <h4>{{playerChoice.label}}</h4>
      </div>
      <div class="flex-item " v-if="winner">
        Computer:
        <img v-bind:src = 'compChoice.image' v-bind:alt = 'compChoice.label'/>
        <h4>{{compChoice.label}}</h4>
      </div>
    </div>
  </div>
</template>

<script>
import choices from './choices'
export default {
  name: 'App',
  components: {},
  data: () => ({
    playerChoices:choices,
    playerChoice:null,
    compChoice:null,
    winner:null}),
  methods: {
    selectChoice(choice) {
      this.playerChoice = choice
      const num = Math.ceil(Math.random()*3 - 1)
      console.log(num)
      this.compChoice = this.playerChoices[num]
      this.checkWinner()
    },
    checkWinner() {
      if(this.playerChoice.value === this.compChoice.value){
        this.winner='Draw!'
      }else if(this.playerChoice.value === 'paper' && this.compChoice.value === "rock"){
        this.winner='Player Won!'
      }else if(this.playerChoice.value === 'rock' && this.compChoice.value === "scissor"){
        this.winner='Player Won!'
      }else if(this.playerChoice.value === 'scissor' && this.compChoice.value === "paper"){
        this.winner='Player Won!'
      }else if(this.compChoice.value === 'paper' && this.playerChoice.value === "rock"){
        this.winner='Computer Won!'
      }else if(this.compChoice.value === 'rock' && this.playerChoice.value === "scissor"){
        this.winner='Computer Won!'
      }else if(this.compChoice.value === 'scissor' && this.playerChoice.value === "paper"){
        this.winner='Computer Won!'
      }
    },
    resetGame() {
      this.playerChoice=null
      this.compChoice=null
      this.winner=''
    }
  }
  }

</script>

<style>
html {
  background-color: #383838;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  margin-top: 60px;
  color: #f4f6f9;
}
.flex-row {
  display: flex;
  justify-content: space-between;
  align-items: center;
}
.flex-item {
  padding: 1em;
  max-height: 12em;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  align-items: center;
  background-color: #303030;
  border-radius: 4px;
  border: 1px solid rgba(255, 255, 255, 0);
  color: #f4f6f9;
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
.winner-circle {
  margin-top: 2em;
  border: 1px solid rgba(255, 255, 255, 0.2);
  padding: 1em;
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