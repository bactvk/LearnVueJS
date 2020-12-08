<template>
	<div class="wrapper-controls">
		<button @click="newGame" class="control btn-new"><i class="ion-ios-plus-outline"></i>New game</button>
		<button @click="rollDice" class="control btn-roll"><i class="ion-ios-loop"></i>Roll dice</button>
		<button @click="$emit('handleHoldScore')" class="control btn-hold"><i class="ion-ios-download-outline"></i>Hold</button>
		<input type="number" placeholder="Final score" class="final-score" v-on:input="$emit('handleChnageFinalScore',$event)" :disabled="isPlaying">
	</div>
</template>
<script type="text/javascript">
	export default{
        name : 'controls',
        data(){
            return {

            }
        },
        props:{
            finalScore:{},
            isPlaying:{},
        },
        methods: {
            newGame(){
               this.$emit("handleNewGame");
            },
            rollDice(){
                console.log('rollDie controls');
                this.$emit('handleRollDice');
            },
            handleInput(e){
                console.log(e.target.value);
            }
        }
    }
</script>
<style type="text/css">
	/**********************************************
*** Control
**********************************************/
.control {
    position: absolute;
    width: 200px;
    left: 50%;
    transform: translateX(-50%);
    color: #555;
    background: none;
    border: none;
    font-family: Lato;
    font-size: 20px;
    text-transform: uppercase;
    cursor: pointer;
    font-weight: 300;
    transition: background-color 0.3s, color 0.3s;
}
.control.disable {
    pointer-events: none;
}

.control:hover { font-weight: 600; }
.control:hover i { margin-right: 20px; }

.control:focus {
    outline: none;
}

.control i {
    color: #42b983;
    display: inline-block;
    margin-right: 15px;
    font-size: 32px;
    line-height: 1;
    vertical-align: text-top;
    margin-top: -4px;
    transition: margin 0.3s;
}

.btn-new { top: 45px;}
.btn-roll { top: 403px;}
.btn-hold { top: 467px;}

.final-score {
    position: absolute;
    left: 50%;
    transform: translateX(-50%);
    top: 520px;
    color: #555;
    font-size: 18px;
    font-family: 'Lato';
    text-align: center;
    padding: 10px;
    width: 160px;
    text-transform: uppercase;
}

.final-score:focus { outline: none; }

</style>