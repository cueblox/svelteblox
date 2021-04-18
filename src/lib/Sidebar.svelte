<script>
	import { page } from '$app/stores';
	export let sections;

	$: active = (sect) => {
		console.log(sect.id, $page.path.includes(sect.id));
		const style = $page.path.includes(sect.id)
			? 'bg-gray-100 text-gray-900'
			: 'bg-white text-gray-600 hover:bg-gray-50 hover:text-gray-900';
		return style;
	};
</script>

<div class="hidden md:flex md:flex-shrink-0">
	<div class="flex flex-col w-64">
		<div
			class="flex flex-col flex-grow border-r border-gray-200 pt-5 pb-4 bg-white overflow-y-auto"
		>
			<div class="flex items-center flex-shrink-0 px-4">
				<img class="h-8 w-auto" src="/logo.svg" alt="Workflow" /><span
					class="px-2 text-base font-semibold tracking-wider text-default-600 uppercase"
				>
					<a href="/">CueBlox</a></span
				>
			</div>
			<div class="mt-5 flex-grow flex flex-col">
				<nav class="flex-1 px-2 bg-white space-y-1">
					<a
						href="/"
						class="bg-white text-gray-600 hover:bg-gray-50 hover:text-gray-900group flex items-center px-2 py-2 text-sm font-medium rounded-md"
					>
						<svg
							class="text-gray-500 mr-3 h-6 w-6"
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
						<!-- Current: "bg-gray-100 text-gray-900", Default: "bg-white text-gray-600 hover:bg-gray-50 hover:text-gray-900" -->

						<a
							href="/{section.id}"
							class="{active(
								section
							)} group flex items-center px-2 py-2 text-sm font-medium rounded-md"
						>
							<!--
                Heroicon name: outline/home
                
                Current: "text-gray-500", Default: "text-gray-400 group-hover:text-gray-500"
                -->
							<!-- Heroicon name: outline/folder -->
							<svg
								class="text-gray-500 mr-3 h-6 w-6 mr-3 h-6 w-6"
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
						<div class="space-y-1" id="sub-menu-3">
							{#each section.pages as page}
								<a
									href="/{section.id}/{page.id}"
									class="group w-full flex items-center pl-10 pr-2 py-2 text-sm font-medium text-gray-600 rounded-md hover:text-gray-900 hover:bg-gray-50"
								>
									{page.title}
								</a>
							{/each}
						</div>
					{/each}
				</nav>
			</div>
		</div>
	</div>
</div>
