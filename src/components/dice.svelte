<script lang="ts">
	import { onMount } from 'svelte';

  let number = 1;
  let rolling = false;

  onMount(()=> {
    getRandomNumber();
  })

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

  function getRandomNumber( ) {
    number = Math.floor(Math.random() * 6) + 1;
  }
</script>

<div class="dice">
  {number}
</div>

<style lang="scss">
  .dice {
    width: 50px;
    height: 50px;
    background-color: gray;
    border: 1px solid black;
    display: flex;
    justify-content: center;
    align-items: center;
    font-size: 24px; 
    font-weight: bold;
  }
</style>
