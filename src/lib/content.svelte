<script>
	export let q_cont;
	let _title = q_cont.title;
	let _type = q_cont.type;

	delete q_cont.title;
	delete q_cont.type;
	let values = Object.keys(q_cont).map((k) => Object.keys(q_cont[k]).map((k2) => q_cont[k][k2]));
</script>

<div>
	{#if _type == 'RadioButton'}
		<h2>{_title}</h2>
		{#each values[0] as inp}
			<label>
				<input type="radio" bind:group={_title} name={inp} value={_title} />
				{inp}
			</label>
		{/each}
	{:else}
		<h2>{_title}</h2>
		{#each values[0] as inp}
			<label>
				<input type="checkbox" />
				{inp}
			</label>
		{/each}
	{/if}
</div>
