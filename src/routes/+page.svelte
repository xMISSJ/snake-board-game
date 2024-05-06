<script lang="ts">
	import { onMount } from 'svelte';
	import Dice from './../components/dice.svelte';
	import Board from '../components/board.svelte';
	import Player from '../components/player.svelte';

	let board;

	const playerCount = 4;
	let playerTurn = 0;
	let players = Array.from({ length: playerCount }, (_, id) => ({ id }));
	let playerRefs: Player[] = [];

	let dice1: Dice;
	let dice2: Dice;

	onMount(() => {
		selectPlayer();
	});

	function rollDices() {
		dice1.rollDice();
		dice2.rollDice();

		playerTurn = (playerTurn + 1) % playerCount;
		selectPlayer();
	}

	function selectPlayer() {
		playerRefs.forEach((playerRef, index) => {
			if (index === playerTurn) {
				playerRef.setSelected();
			} else {
				playerRef.setUnselected();
			}
		});
	}
</script>

<div class="snake-board-game">
	<Board bind:this={board} />

	{#each players as _, id}
		<Player bind:this={playerRefs[id]} {id} {board} />
	{/each}

	<div class="ui-container">
		<div class="dice-container">
			<Dice bind:this={dice1} />
			<Dice bind:this={dice2} />
		</div>

		<button class="roll-button" on:click={rollDices}>Roll</button>

		<p>Player turn: {playerTurn + 1}</p>
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
		cursor: pointer;
		transition: transform 0.3s;

		&:hover {
			transform: scale(1.1);
		}
	}
</style>
