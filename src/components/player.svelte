<script lang="ts">
	import Board from '../components/board.svelte';

	export let id: number;
	export let board: Board;

	let player: any;
	let position = 1;
	let color = 'black';

	export function moveToPosition() {
		player.appendChild(board);
	}

	export function setSelected() {
		color = 'red';
	}

	export function setUnselected() {
		color = 'black';
	}
</script>

<div class="player flex flex-col" style="color: {color};" bind:this={player}>
	<div>웃</div>
	<div>{id}</div>
</div>
