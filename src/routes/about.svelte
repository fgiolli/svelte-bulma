<script context="module">
	import { browser, dev } from '$app/env';
	import Hero from '$lib/hero/Hero.svelte';

	// we don't need any JS on this page, though we'll load
	// it in dev so that we get hot module replacement...
	export const hydrate = dev;

	// ...but if the client-side router is already loaded
	// (i.e. we came here from elsewhere in the app), use it
	export const router = browser;

	// since there's no dynamic data here, we can prerender
	// it so that it gets served as a static asset in prod
	export const prerender = true;
</script>
<svelte:head>
	<title>About</title>
	<meta name="description" content="About this app" />
</svelte:head>

<Hero title="About this app" />

<section class="section">
	<div class="box px-6 px-2" style="color: white;">
	<p>
		This is a <a href="https://kit.svelte.dev">SvelteKit</a> app. You can make your own by typing the
		following into your command line and following the prompts:
	</p>

	<pre class="my-2" style="background-color: #FA7C91; color: black;">git clone https://github.com/fgiolli/svelte-bulma.git
git cd svelte-bulma
npm install</pre>
	
</section>