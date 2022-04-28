<script>
	import FaStopwatch from 'svelte-icons/fa/FaStopwatch.svelte';
	import { mean, median, round } from 'mathjs';

	export let a = () => {};
	export let b = () => {};
	export let executionsToTime = 10;

	const stats = [
		{
			label: 'Min',
			a: '???',
			b: '???'
		},
		{
			label: 'Max',
			a: '???',
			b: '???'
		},
		{
			label: 'Avg',
			a: '???',
			b: '???'
		},
		{
			label: 'Median',
			a: '???',
			b: '???'
		}
	];
	function loadTimingData() {
		const resultsA = getExecutionTimes(a);
		const resultsB = getExecutionTimes(b);
		stats[0].a = `${round(Math.min(...resultsA), 4)} ms`;
		stats[0].b = `${round(Math.min(...resultsB), 4)} ms`;
		stats[1].a = `${round(Math.max(...resultsA), 4)} ms`;
		stats[1].b = `${round(Math.max(...resultsB), 4)} ms`;
		stats[2].a = `${round(mean(...resultsA), 4)} ms`;
		stats[2].b = `${round(mean(...resultsB), 4)} ms`;
		stats[3].a = `${round(median(...resultsA), 4)} ms`;
		stats[3].b = `${round(median(...resultsB), 4)} ms`;
	}

	function getExecutionTimes(fn) {
		var times = [];
		for (let i = 0; i < executionsToTime; i++) {
			var start = performance.now();
			fn();
			var end = performance.now();
			times.push(end - start);
		}
		return times;
	}
</script>

<div class="w-screen flex justify-center">
	<div class="flex flex-col m-6 gap-5">
		<div class="flex justify-center gap-2">
			<button
				on:click={() => a()}
				type="button"
				class="inline-flex items-center px-3 py-2 border border-transparent shadow-md text-sm leading-4 font-medium rounded-md text-white bg-lime-600 hover:bg-lime-700 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-lime-500"
			>
				Run A
			</button>
			<button
				on:click={() => b()}
				type="button"
				class="inline-flex items-center px-3 py-2 border border-transparent shadow-md text-sm leading-4 font-medium rounded-md text-white bg-lime-600 hover:bg-lime-700 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-lime-500"
			>
				Run B
			</button>
		</div>
		<div class="flex justify-center">
			<button
				on:click={() => loadTimingData()}
				type="button"
				class="inline-flex justify-center w-fit items-center px-3 py-2 border border-transparent shadow-md text-sm leading-4 font-medium rounded-md text-white bg-sky-600 hover:bg-sky-700 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-sky-500"
			>
				<div class="w-5 mr-3"><FaStopwatch /></div>
				Time Functions
			</button>
		</div>
		<div class="mt-8 flex flex-col">
			<div class="-my-2 -mx-4 overflow-x-auto sm:-mx-6 lg:-mx-8">
				<div class="inline-block min-w-full py-2 align-middle md:px-6 lg:px-8">
					<div class="overflow-hidden shadow ring-1 ring-black ring-opacity-5 md:rounded-lg">
						<table class="min-w-full divide-y divide-gray-300">
							<thead class="bg-gray-50">
								<tr>
									<th
										scope="col"
										class="py-3.5 pl-4 pr-3 text-left text-sm font-semibold text-gray-900 sm:pl-6"
									/>
									<th
										scope="col"
										class="py-3.5 pl-4 pr-3 text-left text-sm font-semibold text-gray-900 sm:pl-6"
									>
										A
									</th>
									<th
										scope="col"
										class="py-3.5 pl-4 pr-3 text-left text-sm font-semibold text-gray-900 sm:pl-6"
									>
										B
									</th>
								</tr>
							</thead>
							<tbody class="divide-y divide-gray-200 bg-white">
								{#each stats as stat}
									<tr>
										<td
											class="whitespace-nowrap py-4 pl-4 pr-3 text-sm font-medium text-gray-900 sm:pl-6 bg-slate-50 border-r"
										>
											{stat.label}
										</td>
										<td
											class="whitespace-nowrap py-4 pl-4 pr-3 text-sm font-medium text-gray-900 sm:pl-6"
										>
											{stat.a}
										</td>
										<td
											class="whitespace-nowrap py-4 pl-4 pr-3 text-sm font-medium text-gray-900 sm:pl-6"
										>
											{stat.b}
										</td>
									</tr>
								{/each}
							</tbody>
						</table>
					</div>
				</div>
			</div>
		</div>
	</div>
</div>
