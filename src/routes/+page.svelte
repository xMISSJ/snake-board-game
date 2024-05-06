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

<div class="snake-board-game flex justify-between">
	<Board bind:this={board} />

	{#each players as _, id}
		<Player bind:this={playerRefs[id]} {id} {board} />
	{/each}

	<div class="ui-container flex flex-col">
		<div class="dice-container flex mb-[10px]">
			<Dice bind:this={dice1} />
			<Dice bind:this={dice2} />
		</div>

		<button
			class="roll-button w-fit h-fit px-5 py-2.5 bg-gray-500 cursor-pointer transition-transform duration-300 hover:scale-110"
			on:click={rollDices}>Roll</button
		>

		<p>Player turn: {playerTurn + 1}</p>
	</div>
</div>
