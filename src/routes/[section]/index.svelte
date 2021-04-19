<script context="module">
	export const prerender = true;

	import { query, setClient } from 'svelte-apollo';
	import { ApolloClient, InMemoryCache } from '@apollo/client';

	/**
	 * @type {import('@sveltejs/kit').Load}
	 */
	export async function load({ page, session, context }) {
		const graphQLClient = new ApolloClient({
			uri: 'https://api.cueblox.com/api/graphql',
			cache: new InMemoryCache()
		});
		setClient(graphQLClient);
		// const sections = query(`{ allSections { name } }`);

		console.log('SECTIONS');

		const url = `https://cueblox-api.azurewebsites.net/api/sections/${page.params.section}?_embed=pages`;
		const res = await fetch(url);
		if (res.ok) {
			return {
				props: {
					section: await res.json()
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
	export let section;
	import marked from 'marked';
	$: markup = marked(section.body);
</script>

<svelte:head>
	<title>{section.name}</title>
</svelte:head>

<main>
	<h1 class="text-base font-semibold tracking-wider text-indigo-600 uppercase">{section.name}</h1>
	<h2 class="mt-2 text-3xl font-extrabold text-gray-900 tracking-tight sm:text-4xl">
		{section.description}
	</h2>
	<div class="prose lg:prose-xl">
		<p class="pt-2">
			{@html markup}
		</p>
	</div>
	{#each section.pages as page}
		<a href="/{section.id}/{page.id}">{page.title}</a><br />
	{/each}
</main>
