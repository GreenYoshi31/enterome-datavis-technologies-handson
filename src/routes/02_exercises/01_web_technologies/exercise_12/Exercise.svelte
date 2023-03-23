<script>
	let clicked = false;
</script>

<div>
	<button class="btn btn-primary" on:click={() => (clicked = true)}>
		click here
	</button>
	You have 
	{#if clicked}
	   clicked
	{:else}
	   to click 
	{/if}
	the button!
</div>
