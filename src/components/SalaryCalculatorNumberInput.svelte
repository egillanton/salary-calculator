<script lang="ts">
	import { createEventDispatcher } from 'svelte';

	export let label : string = 'No label';
	export let value : number = 0;
	export let percentage : number = 10.0;

	// generate a random label for the input
	export let name : string = Math.random().toString(36).substring(7);
	
	$: total = (value * percentage) / 100.0 || 0.0;

	const dispatch = createEventDispatcher();
	$: dispatch('total', { total });
</script>

<div class="flex flex-col px-6 py-4 border-b border-blue-200 bg-blue-100">
	<label class="text-lg font-semibold" {name} for={name}>{label}</label>
	<div class="flex flex-row flex-none justify-between space-x-4">
		<div class="relative">
			<input
				type="text"
				class=" border border-blue-100 hover:border outline-none hover:border-blue-400 focus:border focus:border-blue-400 w-16 bg-blue-50 rounded pl-1"
				bind:value={percentage}
				id={name}
			/>
			<span class="absolute top-0.5 right-3 ">%</span>
		</div>
		<p class="min-w-[100px] text-right">{total} kr.</p>
	</div>
</div>
