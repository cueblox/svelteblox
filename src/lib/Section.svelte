<script>
	export let section;

	export let path;
	$: current = path.includes(section.id) ? true : false;
	$: buttoncss = current
		? 'text-gray-500 mr-3 h-6 w-6'
		: 'text-gray-400 group-hover:text-gray-500 mr-3 h-6 w-6';
	$: anchorcss = current
		? 'bg-gray-100 text-gray-900'
		: 'text-gray-600 hover:bg-gray-50 hover:text-gray-900';
</script>

<!-- Current: "bg-gray-100 text-gray-900", Default: "text-gray-600 hover:bg-gray-50 hover:text-gray-900" -->

<a
	href="/{section.id}"
	class="{anchorcss} group flex items-center px-2 py-2 text-sm font-medium rounded-md"
>
	<!--
Heroicon name: outline/home

Current: "text-gray-500", Default: "text-gray-400 group-hover:text-gray-500"
-->
	<!-- Heroicon name: outline/folder -->
	<svg
		class="{buttoncss} mr-3 h-6 w-6"
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
