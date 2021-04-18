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
	import MobileMenu from '$lib/MobileMenu.svelte';
	import Sidebar from '$lib/Sidebar.svelte';

	import Search from '$lib/Search.svelte';
	import '../app.postcss';
	export let sections;

	let mobileMenuOpen = true;

	const toggleMenu = () => {
		mobileMenuOpen = !mobileMenuOpen;
	};
</script>

<div class="h-screen flex overflow-hidden bg-gray-100">
	<!-- Off-canvas menu for mobile, show/hide based on off-canvas menu state. -->
	<MobileMenu {sections} bind:hidden={mobileMenuOpen} />

	<!-- Sidebar component, swap this element with another sidebar if you like -->
	<Sidebar {sections} />

	<div class="flex flex-col w-0 flex-1 overflow-hidden">
		<div class="relative z-10 flex-shrink-0 flex h-16 bg-white shadow">
			<button
				on:click={toggleMenu}
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
			<Search />
		</div>

		<main class="flex-1 relative overflow-y-auto focus:outline-none">
			<div class="py-6">
				<div class="max-w-7xl mx-auto px-4 sm:px-6 md:px-8">
					<slot />
				</div>
			</div>
		</main>
	</div>
</div>
