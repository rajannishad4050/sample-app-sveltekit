<script>
	export let sidebarActive;
	export let data;
	export let loading;
	export let errorHappened;
	export let addItemActive;
	export let addedData;

	const fetchData = async (type) => {
		sessionStorage.clear();
		loading = true;
		try {
			const response = await fetch('https://thecocktaildb.com/api/json/v1/1/filter.php?a=' + type);
			if (!response.ok) {
				throw new Error('Failed to fetch data');
				errorHappened = true;
				loading = false;
			}
			const result = await response.json();
			console.log(result, 'result');
			const drinksData = result.drinks;
			if (addedData === undefined) {
				data = drinksData;
			} else {
				data = [...addedData, ...drinksData];
			}
			console.log(data);
			sessionStorage.setItem('myArray', JSON.stringify(data));
			errorHappened = false;
			loading = false;
		} catch (err) {
			console.log(err);
			errorHappened = true;
			loading = false;
		}
	};

	const fetchAlcoholicDrinks = () => {
		fetchData('Alcoholic');
		sidebarActive = false;
	};

	const fetchNon_AlcoholicDrinks = () => {
		fetchData('Non_Alcoholic');
		sidebarActive = false;
	};
</script>

<div class={sidebarActive ? 'sidebar Active' : 'sidebar'}>
	<div class="alchoholic-btn cursor-pointer" on:click={fetchAlcoholicDrinks}>Alchoholic</div>
	<div class="non-alcholic-btn cursor-pointer" on:click={fetchNon_AlcoholicDrinks}>
		Non-Alchoholic
	</div>
	<div
		class="add-items cursor-pointer"
		on:click={() => {
			addItemActive = true;
			sidebarActive = false;
		}}
	>
		Add Item +
	</div>
</div>

<style>
	.sidebar {
		background-color: rgb(32, 127, 185);
		text-align: center;
		color: white;
		height: 100vh;
		width: 40%;
		padding-top: 40px;
		font-size: 1.1rem;
		position: absolute;
		left: -40%;
		transition: 0.3s ease-in-out;
		padding-inline: 20px;
		z-index: 100;
	}

	.Active {
		left: 0;
	}

	.non-alcholic-btn {
		margin-top: 20px;
	}

	.add-items {
		margin-top: 40px;
		text-align: center;
		border: 2px solid white;
		padding: 4px 12;
	}
</style>
