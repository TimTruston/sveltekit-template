<script lang="ts">
	import '../app.css';
	import favicon from '$lib/assets/favicon.svg';
	import Header from './Header.svelte';
	let { children } = $props();
</script>

<svelte:head>
	<link rel="icon" href={favicon} />
</svelte:head>

<div class="app bg-gray-50 text-gray-800 w-full min-h-screen">
<Header/>
{@render children?.()}
</div>