<script lang="ts">
const board: string[][] = []
const width = 10
const height = 10

for (let w = 0; w < width; w++) {
    board[w] = []
    for (let h = 0; h < height; h++) {
        board[w][h] = "*"
    }
}
</script>

<div class="flex col bg-black" style="width: 100px; height: 100px;">
    {#each board as row}
        <div class="flex bg-black">
            {#each row as tile}
                <div class="cell bg-white w-[10px] h-[10px]"></div>
            {/each}
        </div>
    {/each}
</div>