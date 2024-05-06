<script lang="ts">
	import { onMount } from 'svelte';

	let number = 1;
	let rolling = false;

	onMount(() => {
		getRandomNumber();
	});

	export function rollDice() {
		if (!rolling) {
			rolling = true;
			const rollDuration = 500;
			const startTime = Date.now();

			const rollInterval = setInterval(() => {
				const currentTime = Date.now();
				const elapsedTime = currentTime - startTime;

				number = Math.floor(Math.random() * 6) + 1;

				if (elapsedTime >= rollDuration) {
					clearInterval(rollInterval);
					rolling = false;
				}
			}, 100);

			setTimeout(() => {
				getRandomNumber();
				rolling = false;
			}, rollDuration);
		}
	}

	function getRandomNumber() {
		number = Math.floor(Math.random() * 6) + 1;
	}
</script>

<div
	class="dice flex w-[50px] h-[50px] items-center justify-center bg-gray-500 border border-black text-xl font-bold"
>
	{number}
</div>
