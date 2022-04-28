<script>
	import Button from '$lib/leetRaceUI.svelte';

	function run(coins, amount) {
		var coinsUsed = 0;
		var remainingAmount = amount;
		const sortedCoins = coins.sort((a, b) => (a < b ? 1 : -1));
		for (let i = 0; i < coins.length; i++) {
			const numberCurrentCoins = Math.floor(remainingAmount / sortedCoins[i]);
			remainingAmount = remainingAmount % sortedCoins[i];
			coinsUsed += numberCurrentCoins;
			if (remainingAmount === 0) break;
		}
		return remainingAmount === 0 ? coinsUsed : -1;
	}
</script>

<button class="m-6 w-16 bg-red-300" on:click={() => run([1, 2, 5], 11)}>Run</button>
<Button />
