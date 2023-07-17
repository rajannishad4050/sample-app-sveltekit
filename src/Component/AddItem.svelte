<script>
	import Icon from '@iconify/svelte';

	export let data;
	export let addedData;
	export let addItemActive;

	let id = 1;

	let imageUrlInput = '';
	let drinksNameInput = '';

	const addItemInData = () => {
		const newItem = {
			idDrink: 'ss' + id++,
			strDrink: drinksNameInput,
			strDrinkThumb: imageUrlInput
		};

		addedData = addedData.concat(newItem);

		if (data === null) {
			data = [newItem];
			sessionStorage.setItem('myArray', JSON.stringify(data));
		} else {
			data = [newItem, ...data];
			sessionStorage.setItem('myArray', JSON.stringify(data));
		}

		imageUrlInput = '';
		drinksNameInput = '';
		console.log('hello');
	};
</script>

<div class="add-items border-2 bg-slate-700 absolute z-10 px-20 py-10 pb-20">
	<div
		class="cancel text-white flex justify-end cursor-pointer"
		on:click={() => (addItemActive = false)}
	>
		<Icon icon="mdi:cancel-bold" width="30" height="30" />
	</div>
	<h1 class="text-xl text-white">Add Drinks</h1>
	<div class="mt-3">
		<div class="text-white">Image URL (optional)</div>
		<input bind:value={imageUrlInput} class="mt-1" type="text" name="drink-img" />
	</div>
	<div>
		<div class="mt-3 text-white">Drink Name</div>
		<input bind:value={drinksNameInput} class="mt-1" type="text" name="drink-name" />
	</div>
	<button class="bg-slate-500 px-2 py-1 mt-5 text-white" on:click={addItemInData}>submit</button>
</div>

<style>
	.add-items {
		left: calc(50% - 130px);
		top: calc(50% - 140px);
	}
</style>
