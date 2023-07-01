<script>
	export let on = true;
</script>

<div class="light {on === true ? 'on' : ''}" on:click></div>

<style>
	.light {
		width: var(--size, 100px);
		height: var(--size, 100px);
		background-color: gray;
    	border-radius: 10px;
		margin: 5px;
	}

	.on {
		background-color: yellow;
	}
</style>
