<script>
	export let label = '';
	export let styles = '';
	export let handleInput;
	export let value = '';
</script>

<inputContainer class="w-full h-40 flex">
	<label for={label} class={styles}>
		{label}
		<input type="text" class="w-full input" on:input={handleInput} {value} />
	</label>
</inputContainer>

<style>
	inputContainer {
		position: relative;
	}
</style>
