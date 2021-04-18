<script context="module">
	export const prerender = true;
	/**
	 * @type {import('@sveltejs/kit').Load}
	 */
	export async function load({ page, fetch, session, context }) {
		const url = `https://cueblox-api.azurewebsites.net/api/sections/${page.params.section}/pages`;
		const res = await fetch(url);
		if (res.ok) {
			const content = await res.json();
			const pages = content.filter((p) => (p.id = page.params.slug));
			return {
				props: {
					page: pages[0]
				}
			};
		}

		return {
			status: res.status,
			error: new Error(`Could not load ${url}`)
		};
	}
</script>

<script lang="ts">
	export let page;
	import marked from 'marked';
	$: markup = marked(page.body);
</script>

<svelte:head>
	<title>{page.title}</title>
</svelte:head>

<main>
	<h1 class="text-base font-semibold tracking-wider text-indigo-600 uppercase">{page.title}</h1>
	<div class="prose lg:prose-xl">
		<p class="pt-2">
			{@html markup}
		</p>
	</div>
</main>
