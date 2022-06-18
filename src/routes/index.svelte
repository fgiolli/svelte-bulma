<script context="module">
	export const prerender = true;
</script>

<script>
	import Counter from '$lib/Counter.svelte';
	import Hero from '$lib/hero/Hero.svelte';
</script>

<svelte:head>
	<title>Home</title>
	<meta name="description" content="Svelte with bulma demo app" />
</svelte:head>

	<Hero subtitle={'to your new SvelteKit app + Bulma!'}/>
	<Counter />

