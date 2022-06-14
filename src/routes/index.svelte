<script>
	import 'carbon-components-svelte/css/white.css';
	import Box from '$lib/Box.svelte';
	async function getSurvey() {
		let res = await fetch('http://php-server-ksu.run.goorm.io/PHP/', {});
		let survey_db = await res.json();
		return Object.values(survey_db);
	}
	setInterval(getSurvey, 10000);
	let survey = getSurvey();
</script>

<svelte:head>
	<title>Welcome</title>
</svelte:head>

<div>
	{#await survey}
		<h3>Loading.getSurvey..</h3>
	{:then survey_db}
		{#each survey_db as sv_data}
			<Box>
				<a href="/survey/{sv_data.id}">
					{sv_data.title}
				</a>
			</Box>
		{/each}
	{:catch error}
		<p>{error.message}</p>
	{/await}
</div>
