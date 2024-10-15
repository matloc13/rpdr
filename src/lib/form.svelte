<script>
	import TextInput from './textInput.svelte';

	const pages = [{ active: true }, { active: false }, { active: false }];
	let currentPage = pages.findIndex((p) => p.active === true);
	const validated = () => {};

	$: currentPage;
	console.log('currentPage', currentPage);
	let formData = {
		firstName: '',
		lastName: '',
		location: '',
		dateOfRequest: '',
		description: '',
		asset: '',
	};
	console.log('formData', formData);
	const onChange = (e) => {
		e.preventDefault();

		switch (e.submitter.innerText) {
			case 'Next':
				const nextpage = (currentPage += 1);
				pages[currentPage].active = false;
				pages[nextpage].active = true;
				break;
			case 'Back':
				const prevpage = (currentPage -= 1);
				pages[currentPage].active = false;
				pages[prevpage].active = true;
				break;
			case 'Submit':
				break;
			default:
				return null;
		}
	};

	const handleInput = (e) => {
		console.log('e', e);
		console.log('first', e.target.parentElement.htmlFor);
		formData = { ...formData, [e.target.parentElement.htmlFor]: e.target.value };
		console.log('formData', formData);
	};
</script>

<form
	action="post"
	method="post"
	on:submit={onChange}
	class="title-fam bg-gray-light 2xl shadow-xl shadow-red-200 row-start-2 row-span-3 col-start-2 col-span-3 rounded-lg flex flex-col justify-around"
>
	<div>cuurentpage {currentPage + 1}</div>
	{#if currentPage === 0}
		<TextInput
			label="firstName"
			styles="h-100 label w-full"
			{handleInput}
			value={formData.firstName}
		/>
		<TextInput
			label="lastName"
			styles="h-100 label w-full"
			{handleInput}
			value={formData.lastName}
		/>
	{:else if currentPage === 1}
		<TextInput
			label="dateOfRequest"
			styles="h-100 label w-full"
			{handleInput}
			value={formData.dateOfRequest}
		/>
		<TextInput
			label="location"
			styles="h-100 label w-full"
			{handleInput}
			value={formData.location}
		/>
	{:else if currentPage === 2}
		<TextInput
			label="description"
			styles="h-100 label w-full"
			{handleInput}
			value={formData.description}
		/>
		<TextInput label="asset" styles="h-100 label w-full" {handleInput} value={formData.asset} />
	{/if}

	<buttonContainer class="w-full h-40 flex">
		{#if currentPage > 0}
			<label for="back">
				<button class="bg-red-700 rounded-lg" on:change={onChange}> Back </button>
			</label>
		{/if}
		{#if currentPage < pages.length - 1}
			<label for="next">
				<button class="bg-red-700 rounded-lg" on:change={onChange}>Next</button>
			</label>
		{/if}
		{#if currentPage === pages.length - 1}
			<label for="submit">
				<button class="bg-red-700 rounded-lg" on:change={onChange}> Submit </button>
			</label>
		{/if}
	</buttonContainer>
</form>
