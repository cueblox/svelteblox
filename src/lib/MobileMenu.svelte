<script>
	const hide = () => {
		hidden = !hidden;
	};
	export let hidden = false;
	export let sections;
</script>

<div
	class="{hidden ? 'hidden' : ''}
fixed inset-0 flex z-40 md:hidden"
	role="dialog"
	aria-modal="true"
>
	<div class="fixed inset-0 bg-gray-600 bg-opacity-75" aria-hidden="true" />
	<div class="relative flex-1 flex flex-col max-w-xs w-full pt-5 pb-4 bg-white">
		<div class="absolute top-0 right-0 -mr-12 pt-2">
			<button
				on:click={hide}
				class="ml-1 flex items-center justify-center h-10 w-10 rounded-full focus:outline-none focus:ring-2 focus:ring-inset focus:ring-white"
			>
				<span class="sr-only">Close sidebar</span>
				<!-- Heroicon name: outline/x -->
				<svg
					class="h-6 w-6 text-white"
					xmlns="http://www.w3.org/2000/svg"
					fill="none"
					viewBox="0 0 24 24"
					stroke="currentColor"
					aria-hidden="true"
				>
					<path
						stroke-linecap="round"
						stroke-linejoin="round"
						stroke-width="2"
						d="M6 18L18 6M6 6l12 12"
					/>
				</svg>
			</button>
		</div>

		<div class="flex-shrink-0 flex items-center px-4">
			<img class="h-8 w-auto" src="/logo.svg" alt="Workflow" />
		</div>
		<div class="mt-5 flex-1 h-0 overflow-y-auto">
			<nav class="px-2 space-y-1">
				<!-- Current: "bg-gray-100 text-gray-900", Default: "text-gray-600 hover:bg-gray-50 hover:text-gray-900" -->
				<a
					href="/"
					class="bg-gray-100 text-gray-900 group flex items-center px-2 py-2 text-base font-medium rounded-md"
				>
					<svg
						class="text-gray-500 mr-4 h-6 w-6"
						xmlns="http://www.w3.org/2000/svg"
						fill="none"
						viewBox="0 0 24 24"
						stroke="currentColor"
						aria-hidden="true"
					>
						<path
							stroke-linecap="round"
							stroke-linejoin="round"
							stroke-width="2"
							d="M3 12l2-2m0 0l7-7 7 7M5 10v10a1 1 0 001 1h3m10-11l2 2m-2-2v10a1 1 0 01-1 1h-3m-6 0a1 1 0 001-1v-4a1 1 0 011-1h2a1 1 0 011 1v4a1 1 0 001 1m-6 0h6"
						/>
					</svg>
					Home
				</a>
				{#each sections as section}
					<a
						href={section.id}
						class="text-gray-600 hover:bg-gray-50 hover:text-gray-900 group flex items-center px-2 py-2 text-base font-medium rounded-md"
					>
						<!-- Heroicon name: outline/folder -->
						<svg
							class="text-gray-400 group-hover:text-gray-500 mr-4 h-6 w-6"
							xmlns="http://www.w3.org/2000/svg"
							fill="none"
							viewBox="0 0 24 24"
							stroke="currentColor"
							aria-hidden="true"
						>
							<path
								stroke-linecap="round"
								stroke-linejoin="round"
								stroke-width="2"
								d="M3 7v10a2 2 0 002 2h14a2 2 0 002-2V9a2 2 0 00-2-2h-6l-2-2H5a2 2 0 00-2 2z"
							/>
						</svg>
						{section.name}
					</a>
				{/each}
			</nav>
		</div>
	</div>

	<div class="flex-shrink-0 w-14" aria-hidden="true">
		<!-- Dummy element to force sidebar to shrink to fit close icon -->
	</div>
</div>
