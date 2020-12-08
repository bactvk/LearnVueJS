<template>
  <div id="app">
    <h1>Dice Game</h1>
    <div class="wrapper clearfix">
      <Players :scorePlayer="scorePlayer" :currentScore="currentScore" :activePlayer="activePlayer" :isWinner="isWinner">
      </Players>
      <Controls @handleNewGame="handleNewGame" @handleRollDice="handleRollDice" @handleHoldScore="handleHoldScore" :finalScore="finalScore" @handleChnageFinalScore="handleChnageFinalScore"></Controls>
      <Dices :dices="dices"></Dices>
      <PopupRule :isOpenPopup="isOpenPopup" @handleConfirm="handleConfirm" />
    </div>
  </div>
</template>

<script>

import Players from './components/Players.vue';
import Controls from './components/Controls.vue';
import Dices from './components/Dices.vue';
import PopupRule from './components/PopupRule.vue';
export default {
  name: 'App',
  data(){
    return {
      isPlaying: false,
      isOpenPopup: false,
      activePlayer: 0, // Who is current player?
      scorePlayer: [0,0],
      currentScore: 0,
      dices : [1,1],
      finalScore : 15
    }
  },
  components: {
    Players,
    Controls,
    Dices,
    PopupRule
  },
  computed:{
    isWinner(){
      let { scorePlayer, finalScore } = this;
      if(scorePlayer[0] >= finalScore || scorePlayer[1] >= finalScore){
        // Dung cuoc choi
        // this.isPlaying = false;
        return true;
      }
      return false;
    }
  },
  methods:{
    nextPlayer(){
      //activePlayer = 0 -> 1
      this.activePlayer = this.activePlayer == 0 ? 1 : 0;
      this.currentScore = 0;
    },
    handleNewGame(){
      // show popup
      console.log("show popup");
      this.isOpenPopup = true;
    },
    handleConfirm(){
      console.log("close popup");
      this.isPlaying = true;
      this.isOpenPopup = false;
      this.activePlayer = 0;
      this.scorePlayer = [0,0];
      this.currentScore = 0;
      this.dices = [1,1];
    },
    handleRollDice(){
      console.log('handleRollDice');
      if(this.isPlaying){
        // xoay xuc sac
        // Math.random() : 0 -> 1
        /*
          0 <= X <= 1
          0*6 <= y= x*6 <= 6
        */
        var dice1 = Math.floor(Math.random()*6 + 1);
        var dice2 = Math.floor(Math.random()*6 + 1);

        this.dices = [dice1,dice2];
        if(dice1 == 1 || dice2 == 1){
          let activePlayer = this.activePlayer; 
          setTimeout(function() {
            alert("Mất lượt chơi. Người chơi "+ ( activePlayer + 1)+" đã quay trúng số 1.");
          },10)
          // Đỗi lượt chơi
          this.nextPlayer();
        }else{
          // cộng dồn
          this.currentScore += dice1 + dice2;
        }

      }else{
        alert("Please click new Game");
      }
    },
    handleHoldScore(){
      if(this.isPlaying){
        let {scorePlayer , activePlayer, currentScore } = this;
        let scoreOld = scorePlayer[activePlayer];

        let cloneScorePlayer = [...scorePlayer];
        cloneScorePlayer[activePlayer] = scoreOld + currentScore;

        this.scorePlayer = cloneScorePlayer;
        
        if(!this.isWinner){
          this.nextPlayer();
        }
      }else{
        alert("Please click new Game");
      }
    },

    handleChnageFinalScore(e){
      console.log(e.target.value);
    }

  },
  watch:{
    isWinner(){
      let { scorePlayer, finalScore } = this;
      if(scorePlayer[0] >= finalScore || scorePlayer[1] >= finalScore){
        // Dung cuoc choi
        this.isPlaying = false;
      }
    }
  }
  
}
</script>

<style>
  /**********************************************
*** GENERAL
**********************************************/
* {
    margin: 0;
    padding: 0;
    box-sizing: border-box; 
}

.clearfix::after {
    content: "";
    display: table;
    clear: both;
}

body {
    background-image: linear-gradient(rgba(62, 20, 20, 0.4), rgba(62, 20, 20, 0.4)), url('assets/back.jpg');
    background-size: cover;
    background-position: center;
    font-family: Lato;
    font-weight: 300;
    position: relative;
    height: 100vh;
    color: #555;
}

.wrapper {
    width: 1000px;
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    background-color: #fff;
    box-shadow: 0px 10px 50px rgba(0, 0, 0, 0.3);
    overflow: hidden;
}
  

</style>
