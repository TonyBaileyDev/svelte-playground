<script>
	import {v4 as uuidv4} from 'uuid';
	
	export let maxGenerated = 100;
	export let initialUuidCount = 3;
	export let showDescription = true;
	
  let uuids = "";
	let amount = 1;
	
	function generate(count) {
		for (let i = 0; i < count; i++) {
		  uuids += uuidv4() + "\n";
		}
	}

	function generateClicked() {
		if (isNaN(amount) || amount < 0) {
			amount = 1;
		}

		if (amount > maxGenerated) {
			amount = maxGenerated;
		}
		
		generate(Number(amount));
	}
	
	function clearClicked() {
		 uuids = "";
	}

	generate(initialUuidCount)
</script>


{#if showDescription}
	<h2>UUID Generator</h2>
	<p>Generate some UUIDs.</p>
{/if}

<button on:click={generateClicked}>Generate</button>
<input type="text" bind:value={amount} />
<br />
<textarea>{uuids}</textarea>
<br />
<button on:click={clearClicked}>Clear</button>


<style>
	textarea {
		width: 100%;
		height: 300px;
		resize: none;
	}
</style>