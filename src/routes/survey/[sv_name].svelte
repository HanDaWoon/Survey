<!-- src/routes/blog/[slug].svelte -->
<script context="module">
	import { page } from '$app/stores';
	// the (optional) preload function takes a
	// `{ path, params, query }` object and turns it into
	// the data we need to render the page
	export async function preload(page, session) {
		// the `slug` parameter is available because this file
		// is called [slug].svelte
		const { slug } = page.params;

		// `this.fetch` is a wrapper around `fetch` that allows
		// you to make credentialled requests on both
		// server and client
		const res = await this.fetch(`blog/${slug}.json`);
		const article = await res.json();

		return { article };
	}
</script>

<script>
	// export let article;
</script>

{$page.params.sv_name}


<!-- 
<script>
	export let svdb;
	import Content from '../../lib/content.svelte';

	let _title = svdb.title;
	let _id = svdb.id;

	delete svdb.title;
	delete svdb.id;
	const _svdb = Object.values(svdb);
</script>

<svelte:head>
	<title>Survey</title>
</svelte:head>

<div>
	<div>
		<h3>{_title}</h3>
		<h5>{_id}</h5>
	</div>
	<div>
		{#each _svdb as q_cont}
			<Content {q_cont} />
		{/each}
	</div>
</div> -->
