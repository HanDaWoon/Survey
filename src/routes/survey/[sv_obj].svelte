<script>
	import { page } from '$app/stores';
	import Box from '../../lib/Box.svelte';
	const sv_id = $page.params.sv_obj;
	let survey = [];
	let poll_content = [];
	async function getSurvey() {
		let res = await fetch('http://php-server-ksu.run.goorm.io/PHP/', {});
		let survey_db = await res.json();

		survey = Object.values(survey_db);
		survey = survey.filter((v) => v.id == sv_id);
		return survey;
	}
	getSurvey();
	import Content from '../../lib/content.svelte';

	let _title = '';
	let _id = '';
	$: if (survey.length > 0) {
		_title = survey[0].title;
		_id = survey[0].id;

		delete survey[0].title;
		delete survey[0].id;

		poll_content = Object.values(survey[0]);
	}
	function save_alert() {
		alert('설문에 응해주셔서 감사합니다!');
	}
</script>

<svelte:head>
	<title>Survey</title>
</svelte:head>
<div>
	<div class="hero is-small has-background-success-light">
		<div class="hero-body">
			<h3 class="subtitle">{_title}</h3>
		</div>
	</div>
	<div class="section">
		<div class="conatiner">
			<div>
				{#each poll_content as q_cont}
					<Box><Content {q_cont} /></Box>
				{/each}
			</div>
			<div style="text-align:center">
				<button class="button is-success" on:click={save_alert}>저장</button>
			</div>
		</div>
	</div>
</div>
