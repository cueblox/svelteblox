<script context="module">
	/**
	 * @type {import('@sveltejs/kit').Load}
	 */
	export async function load({ page, fetch, session, context }) {
		const url = `https://cueblox-api.azurewebsites.net/api/sections/?_sort=weight&_embed=pages`;
		const res = await fetch(url);
		const sections = await res.json();
		if (res.ok) {
			return {
				context: {
					sections: sections
				},
				props: {
					sections: sections,
					path: page.path
				}
			};
		}

		return {
			status: res.status,
			error: new Error(`Could not load ${url}`)
		};
	}
</script>

<script>
	import { page } from '$app/stores';
	import MobileMenu from '$lib/MobileMenu.svelte';
	import Sidebar from '$lib/Sidebar.svelte';
	import '../app.postcss';
	export let sections;
	export let path;

	import { createEventDispatcher } from 'svelte'
  	const dispatch = createEventDispatcher()

	let mobileMenuOpen = true;

	const toggleMenu = () => {
		mobileMenuOpen = !mobileMenuOpen
	}	
</script>

<div class="h-screen flex overflow-hidden bg-gray-100">
	<!-- Off-canvas menu for mobile, show/hide based on off-canvas menu state. -->
	<MobileMenu bind:hidden={mobileMenuOpen}/>

	<!-- Sidebar component, swap this element with another sidebar if you like -->
	<div class="hidden md:flex md:flex-shrink-0">
		<div class="flex flex-col w-64">
			<div
				class="flex flex-col flex-grow border-r border-gray-200 pt-5 pb-4 bg-white overflow-y-auto"
			>
				<div class="flex items-center flex-shrink-0 px-4">
					<img class="h-8 w-auto" src="/logo.svg" alt="Workflow" /><span class="px-2 text-base font-semibold tracking-wider text-default-600 uppercase">
						<a href="/">CueBlox</a></span>
				</div>
				<div class="mt-5 flex-grow flex flex-col">
					<nav class="flex-1 px-2 bg-white space-y-1">
						{#each sections as section}
						<a
						href="/{section.id}"
						class="bg-gray-100 text-gray-900 group flex items-center px-2 py-2 text-sm font-medium rounded-md"
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
								<a href="/{section.id}/{page.id}" class="group w-full flex items-center pl-10 pr-2 py-2 text-sm font-medium text-gray-600 rounded-md hover:text-gray-900 hover:bg-gray-50">
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
	

	<div class="flex flex-col w-0 flex-1 overflow-hidden">
		<div class="relative z-10 flex-shrink-0 flex h-16 bg-white shadow">
			<button on:click={toggleMenu}
				class="px-4 border-r border-gray-200 text-gray-500 focus:outline-none focus:ring-2 focus:ring-inset focus:ring-indigo-500 md:hidden"
			>
				<span class="sr-only">Open sidebar</span>
				<!-- Heroicon name: outline/menu-alt-2 -->
				<svg
					class="h-6 w-6"
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
						d="M4 6h16M4 12h16M4 18h7"
					/>
				</svg>
			</button>
			<div class="flex-1 px-4 flex justify-between">
				<div class="flex-1 flex">
					<form class="w-full flex md:ml-0" action="#" method="GET">
						<label for="search_field" class="sr-only">Search</label>
						<div class="relative w-full text-gray-400 focus-within:text-gray-600">
							<div class="absolute inset-y-0 left-0 flex items-center pointer-events-none">
								<!-- Heroicon name: solid/search -->
								<svg
									class="h-5 w-5"
									xmlns="http://www.w3.org/2000/svg"
									viewBox="0 0 20 20"
									fill="currentColor"
									aria-hidden="true"
								>
									<path
										fill-rule="evenodd"
										d="M8 4a4 4 0 100 8 4 4 0 000-8zM2 8a6 6 0 1110.89 3.476l4.817 4.817a1 1 0 01-1.414 1.414l-4.816-4.816A6 6 0 012 8z"
										clip-rule="evenodd"
									/>
								</svg>
							</div>
							<input
								id="search_field"
								class="block w-full h-full pl-8 pr-3 py-2 border-transparent text-gray-900 placeholder-gray-500 focus:outline-none focus:placeholder-gray-400 focus:ring-0 focus:border-transparent sm:text-sm"
								placeholder="Search"
								type="search"
								name="search"
							/>
						</div>
					</form>
				</div>
			</div>
		</div>

		<main class="flex-1 relative overflow-y-auto focus:outline-none">
			<div class="py-6">
				<div class="max-w-7xl mx-auto px-4 sm:px-6 md:px-8">
					<slot ></slot>
				</div>
			</div>
		</main>
	</div>
</div>
