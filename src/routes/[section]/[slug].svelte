<script context="module">
	export const prerender = true;
	/**
	 * @type {import('@sveltejs/kit').Load}
	 */
	export async function load({ page, fetch, session, context }) {
		const url = `https://cueblox-api.azurewebsites.net/api/pages/${page.params.slug}`;
		const res = await fetch(url);
		if (res.ok) {
			return {
				props: {
					content: await res.json()
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
	export let content;
	import marked from 'marked';
	$: markup = marked(content.body);
</script>

<svelte:head>
	<title>{content.title}</title>
</svelte:head>

<main>
	<h1 class="text-base font-semibold tracking-wider text-indigo-600 uppercase">{content.title}</h1>
	<div class="prose lg:prose-xl">
		<p class="pt-2">
			{@html markup}
		</p>
	</div>
</main>
