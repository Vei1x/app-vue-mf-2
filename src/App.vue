<template>
  <div class="clicker">
    <p class="score" :style="{ backgroundColor: scoreColor, fontSize: scoreFontSize + 'px' }">{{ score }}</p>
    <div v-if="gameOver">
      <button class="reset-button" @click="resetGame">Your score is {{ score }}. Click to reset</button>
    </div>
    <div class="button-container" v-else>
      <button class="smash-button" @click="handleClick">SMASH</button>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      score: 0,
      gameOver: false,
    };
  },
  computed: {
    scoreColor() {
      const redPercentage = Math.min(this.score, 100);
      return `hsl(${360 * (1 - (redPercentage / 100))}, 100%, ${50 + (50 * (1 - (redPercentage / 100)) )}%)`;
    },
    scoreFontSize() {
      return this.score > 99 ? 60 : 80; // adjust the sizes as needed
    },
  },
  methods: {
    handleClick() {
      if (this.gameOver) {
        this.resetGame();
      } else {
        this.score++;
        if (this.score === 100) {
          this.gameOver = true;
        }
      }
    },
    resetGame() {
      this.score = 0;
      this.gameOver = false;
    },
  },
};
</script>

<style>
* {
  margin: 0;
  padding: 0;
}

.score {
  margin: 20%;
  text-align: center;
  font-size: 80px;
  animation: boom 0.1s linear;
  color:black;
  border: 1px grey solid;
  border-radius: 10px;
  background-color: grey;
}

.button-container {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100px;
}

.smash-button {
  padding: 25px;
  font-size: 20px;
  border-radius: 10px;
  border: 2px black solid;
}

.clicker {
  justify-content: center;
  align-items: center;
  margin: auto;
  margin-top: 10px;
  border: 2px black solid;
  border-radius: 10px;
  width: 20%;
  background-color: black;
}

.smash-button:active {
  background-color: red;
  animation: smash 0.1s linear;
  color: white;
  animation: smashcolor 0.1s linear;
}

@keyframes smash {
  0% {
    transform: scale(1);
  }
  50% {
    transform: scale(1.2);
  }
  100% {
    transform: scale(1);
  }
}

@keyframes smashcolor {
  0% {
    background-color: red;
    font-size: 35px;
  }
  100% {
    background-color: rgb(141, 9, 9);
  }
}

.reset-button {
  /* your custom styles for the reset button */
  display: flex;
  margin: auto;
  margin-bottom: 10px;
  padding: 25px;
  font-size: 20px;
  border-radius: 10px;
  border: 2px black solid;
}
</style>