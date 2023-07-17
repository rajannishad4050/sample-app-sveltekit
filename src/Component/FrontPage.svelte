<script>
	import Icon from '@iconify/svelte';

	export let data;
	export let loading;
	export let errorHappened;
</script>

{#if data === null && loading === false && errorHappened === false}
	<main class="flex items-center justify-center">
		<h2 class="mt-40 text-xl font-semibold">Select from sidebar to Get the data on this page</h2>
	</main>
{:else if loading === true}
	<div class="absolute left-[45%] top-[40%]">Loading...</div>
{:else if errorHappened === true}
	<div class="text-2xl absolute left-[50%] right-[50%] top-[40%]">404 Not found</div>
{:else}
	<div class="main-grid px-20 py-14">
		{#each data as item}
			<div class="card cursor-pointer">
				<a href={'/' + item.idDrink}>
					{#if item.strDrinkThumb === ''}
						<img
							class="card-img"
							src="https://www.thecocktaildb.com/images/media/drink/ypxsqy1483387829.jpg"
							alt=""
							loading="lazy"
						/>
					{:else}
						<img class="card-img" src={item.strDrinkThumb} alt="" loading="lazy" />
					{/if}
					<div class="title p-2 text-center font-semibold">{item.strDrink}</div>
				</a>
			</div>
		{/each}
	</div>
{/if}

<style>
	.main-grid {
		display: grid;
		grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
		gap: 1.5rem;
	}

	.card-img {
		border-radius: 1rem;
	}
</style>
