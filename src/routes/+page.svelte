<script lang="ts">
  	import { onMount } from 'svelte';
	import Dice from './../components/dice.svelte';
    import Board from "../components/board.svelte";
    import Player from "../components/player.svelte";

    let board

    const playerCount = 4;
    let playerTurn = 0;
    let players : any[] = [];
    let playerRefs : Player[] = [];

    let dice1: Dice;
    let dice2: Dice;

    onMount(()=> {
      players = Array.from({ length: playerCount }, (_, id) => ({ id }));

      selectPlayer();
    })

    function rollDices(){
        dice1.rollDice();
        dice2.rollDice();

        if (playerTurn >= playerCount) {
          playerTurn = 0;
          return;
        }

        playerTurn++;
        selectPlayer();
    }

    function selectPlayer(){
      playerRefs.forEach((playerRef, index) => {
        console.log("Index: " + index + " playerTurn: " + playerTurn);
        if (index + 1 === playerTurn) {
          playerRef.setSelected();
          return;
        } 

          playerRef.setUnselected();
      });
    }
</script>

<div class="snake-board-game">
    <Board bind:this={board}/>

    {#each players as _, id}
        <Player bind:this={playerRefs[id]} id={id} board={board}/>
    {/each}

    <div class="ui-container">
        <div class="dice-container">
            <Dice bind:this={dice1}/>
            <Dice bind:this={dice2}/>
        </div>

        <div class="roll-button" on:click={()=> rollDices()}>Roll</div>

        <p>Player turn: {playerTurn}</p>
    </div>
</div>

<style lang="scss">
    .snake-board-game {
        display: flex;
        justify-content: space-between;
    }

    .ui-container {
        display: flex;
        flex-direction: column;
    }

    .dice-container {
        display: flex;
        margin-bottom: 10px;
    }

    .roll-button {
        width: fit-content;
        height: fit-content;
        padding: 10px 20px;
        background-color: grey;
        transition: transform 0.3s;
        cursor: pointer;

        &:hover {
            transform: scale(1.1);
        }
    }
</style>


