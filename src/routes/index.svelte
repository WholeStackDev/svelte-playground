<script>
	import LeetRaceUI from '$lib/leetRaceUI.svelte';

	const coins = [1, 2, 5];
	const amount = 11;

	function a() {
		var coinsUsed = 0;
		var remainingAmount = amount;
		const sortedCoins = coins.sort((a, b) => (a < b ? 1 : -1));
		for (let i = 0; i < coins.length; i++) {
			const numberCurrentCoins = Math.floor(remainingAmount / sortedCoins[i]);
			remainingAmount = remainingAmount % sortedCoins[i];
			coinsUsed += numberCurrentCoins;
			if (remainingAmount === 0) break;
		}
		console.log(remainingAmount === 0 ? coinsUsed : -1);
		wait(100);
		return remainingAmount === 0 ? coinsUsed : -1;
	}
	function b() {
		var test = 0;
		for (let i = 0; i < 1000000; i++) {
			test++;
		}
	}

	function wait(ms) {
		var start = Date.now(),
			now = start;
		while (now - start < ms) {
			now = Date.now();
		}
	}
</script>

<LeetRaceUI {a} {b} />
