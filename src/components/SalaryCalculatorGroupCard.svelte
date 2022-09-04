<script lang="ts">
	export let title : string = 'No title';
	export let description : string = 'No description';
</script>

<div
	class="max-w-sm rounded overflow-hidden shadow-lg border border-blue-200">
	<div class="px-6 py-4">
		<div class="font-bold text-xl mb-2">{title}</div>
		<div class="text-gray-700 text-base truncate">{description}</div>
	</div>
	<slot>No content</slot>
</div>
