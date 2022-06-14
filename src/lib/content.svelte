<script>
	export let q_cont;
	let _title = q_cont.title;
	let _type = q_cont.type;

	delete q_cont.title;
	delete q_cont.type;
	let values = Object.keys(q_cont).map((k) => Object.keys(q_cont[k]).map((k2) => q_cont[k][k2]));
</script>

<div>
	<h2 class="subtitle">{_title}</h2>
	{#if _type == 'RadioButton'}
		{#each values[0] as inp}
			<label class="mr-4">
				<input type="radio" bind:group={_title} name={inp} value={_title} />
				{inp}
			</label>
		{/each}
	{:else}
		{#each values[0] as inp}
			<label class="mr-4">
				<input type="checkbox" />
				{inp}
			</label>
		{/each}
	{/if}
	
</div>
