<script lang="ts">
	const board: string[][] = [];
	const row = 10;
	const column = 10;

    for (let c = 0; c < column; c++) {
        board[c] = [];
        for (let r = 0; r < row; r++) {
		    board[c][r] = '*';
	    }
    }
</script>

<style lang="scss">
.grid {
  background-color: #d8c5a1;
}

.grid-row {
    display: flex;
}

.grid-cell {
    width: 100%
}

.grid-row:nth-child(even) .grid-cell:nth-child(even) {
    background-color: #51280c;
}

.grid-row:nth-child(odd) .grid-cell:nth-child(odd) {
    background-color: #51280c;
}
</style>
<div class="grid w-[1000px] h-[1000px] border border-black overflow-hidden">
    {#each board as row, rowIndex}
        <div class="grid-row" key="row-{rowIndex}">
            {#if rowIndex % 2 === 0}
                {#each row as tile, tileIndex}
                    <div class="text-white text-xl text-center drop-shadow-[0_1.2px_1.2px_rgba(0,0,0,0.8)] grid-cell flex w-1000 w-[100px] h-[100px]" key="tile-{((9 - rowIndex) * 10) + (9 - tileIndex) + 1}">
                        {((9 - rowIndex) * 10) + (9 - tileIndex) + 1}
                    </div>
                {/each}
            {:else}
                {#each row as tile, tileIndex}
                    <div class="text-white text-xl text-center drop-shadow-[0_1.2px_1.2px_rgba(0,0,0,0.8)] grid-cell flex w-1000 w-[100px] h-[100px]" key="tile-{((9 - rowIndex) * 10) + tileIndex + 1}">
                        {((9 - rowIndex) * 10) + tileIndex + 1}
                    </div>
                {/each}
            {/if}
        </div>
    {/each}
</div>