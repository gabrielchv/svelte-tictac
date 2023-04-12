<script>
	let tictac = [
		["", "", ""],
		["", "", ""],
		["", "", ""],
	];
	let playNum = 0;
	
	$: player = playNum % 2 === 0 ? "x" : "o";
	
	const reset = () => {
		for (let i = 0; i < tictac.length; i++) {
			for (let j = 0; j < tictac[i].length; j++) {
				tictac[i][j] = "";
			}
		}
		playNum = 0;
	}
	
	const checkVictory = (tictac) => {
    for (let i = 0; i < 3; i++) {
			if (tictac[i][0] === tictac[i][1] && tictac[i][1] === tictac[i][2] && tictac[i][0] !== "") {
				playNum--;
				return true;
			}
			if (tictac[0][i] === tictac[1][i] && tictac[1][i] === tictac[2][i] && tictac[0][i] !== "") {
				playNum--;  
				return true;
			}
    }
    if (tictac[0][0] === tictac[1][1] && tictac[1][1] === tictac[2][2] && tictac[1][1] !== "") {
    	playNum--;
			return true;
    }
    if (tictac[2][0] === tictac[1][1] && tictac[1][1] === tictac[0][2] && tictac[1][1] !== "") {
    	playNum--;
			return true;
    }
    return false;
	}
	
	const onClick = (i, j) => {
		if (!tictac[i][j] && !checkVictory(tictac)) {
			playNum++;
			tictac[i][j] = player;
		}
	}
</script>

{#if checkVictory(tictac)}
<div>Vencedor: {player}</div>
{:else}
<span>Vez de: {player}</span>
{/if}
<div class="flex flex-col">
{#each tictac as line, i}
	<div class="flex">
	{#each line as token, j}
			<button on:click={() => onClick(i, j)} class="border rounded-none border-black w-6 h-6 text-center">{token}</button>
	{/each}
	</div>
{/each}
</div>
<button on:click={reset} class="bg-red-500 text-white font-bold py-1 px-2 rounded">
	Resetar
</button>


<svelte:head>
<link rel="stylesheet" href="https://unpkg.com/tailwindcss@2.2.19/dist/tailwind.min.css"/>
</svelte:head>
