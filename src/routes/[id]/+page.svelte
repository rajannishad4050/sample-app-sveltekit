<script>
	import Icon from '@iconify/svelte';
	import { page } from '$app/stores';

	const cocktailDetails = null;

	const id = $page.params.id;

	const loadData = async () => {
		try {
			const response = await fetch('https://thecocktaildb.com/api/json/v1/1/lookup.php?i=' + id);
			const data = await response.json();
			return data.drinks[0];
		} catch (err) {
			console.log(err);
		}
	};
</script>

{#if id.charAt(0) === 's'}
	<header class="flex justify-between px-5 py-2">
		<a href="/">
			<Icon icon="eva:arrow-back-outline" class="cursor-pointer" width="32" height="32" />
		</a>
		<a href="/">
			<div class="border-2 px-4 py-1.5 cursor-pointer">Back Home</div>
		</a>
	</header>
	<div class="mt-12 gap-10 px-12 max-w-[1000px] mx-auto sm:flex">
		<img
			class="h-[300px] mx-auto sm:w-[40%]"
			src="https://www.thecocktaildb.com/images/media/drink/ypxsqy1483387829.jpg"
			alt=""
			loading="lazy"
		/>
		<div class="discription mt-4 text-center sm:w-[60%] sm:text-center text-xl self-center sm:mt-0">
			No Info
		</div>
	</div>
{:else}
	{#await loadData()}
		<h1 class="absolute left-[50%] right-[50%] top-[40%]">Loading...</h1>
	{:then data}
		<header class="flex justify-between px-5 py-2">
			<a href="/">
				<Icon icon="eva:arrow-back-outline" class="cursor-pointer" width="32" height="32" />
			</a>
			<a href="/">
				<div class="border-2 px-4 py-1.5 cursor-pointer">Back Home</div>
			</a>
		</header>
		<h1 class="text-center text-[1.6rem] mt-10 sm:mt-1">{data.strDrink}</h1>
		<div class="mt-12 gap-10 px-12 max-w-[1000px] mx-auto sm:flex">
			<img class="h-[300px] mx-auto sm:w-[40%]" src={data.strDrinkThumb} alt="" />
			<div class="discription mt-4 text-center sm:w-[60%] sm:text-left sm:mt-0">
				<div>
					<span>Type :</span>
					{data.strAlcoholic}
				</div>
				<p class="mt-4">{data.strInstructions}</p>
				<div class="mt-4">
					<span>Ingrideints :</span>
					{data.strIngredient1}, {data.strIngredient2}, {data.strIngredient3}
				</div>
			</div>
		</div>
	{:catch error}
		<p>an error has occured</p>
	{/await}
{/if}
