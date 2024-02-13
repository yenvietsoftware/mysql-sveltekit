<script>
	export let data;
	let res;
	let statedata = '';
	async function xget(st) {
		const response = await fetch('/api/getserver', {
			method: 'POST',
			body: JSON.stringify({ st }),
			headers: {
				'content-type': 'application/json'
			}
		});

		res = await response.json();
		statedata = res[0];
	}
</script>

<h1>Get State Information</h1>
<p>Click state name to see data at bottom.</p>
{#each data.data as state}
    <button on:click={() => xget(state.state)}>{state.state}</button>
{/each}
{#if statedata}
    <p>The capital of {statedata.state} is {statedata.capital}!</p>
    <p>Its abbreviation is {statedata.abbr}.</p>
    <p>It is in the {statedata.region} region.</p>
    <p>Its state bird is the {statedata.bird}.</p>
{/if}

<style>
	button,
	p {
		padding: 0.5em 0.8em;
		margin: 0.5em;
		font-size: 110%;
	}
</style>
