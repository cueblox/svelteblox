<script>
	import Section from './Section.svelte';

	export let hidden;
	export let sections;
	export let path;
</script>

<div class="{hidden ? 'hidden' : ''} md:flex md:flex-shrink-0">
	<div class="flex flex-col w-64">
		<div
			class="flex flex-col flex-grow border-r border-gray-200 pt-5 pb-4 bg-white overflow-y-auto"
		>
			<div class="flex items-center flex-shrink-0 px-4">
				<img class="h-8 w-auto" src="/logo.svg" alt="Workflow" />
			</div>
			<div class="mt-5 flex-grow flex flex-col">
				<nav class="flex-1 px-2 bg-white space-y-1">
					{#each sections as section}
						<Section {section} bind:path />
					{/each}
				</nav>
			</div>
		</div>
	</div>
</div>
