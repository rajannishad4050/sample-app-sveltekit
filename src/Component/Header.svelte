<script>
	export let sidebarActive;
	import Icon from '@iconify/svelte';
	export let data;

	let inputValue = '';

	const visibleSideBar = () => {
		sidebarActive = !sidebarActive;
	};

	const enterKeyPressed = (event) => {
		if (event.key === 'Enter') {
			visibleSideBar();
		}
	};

	const searchData = () => {
		const filterData = data.filter((item) =>
			item.strDrink.toLowerCase().slice(0, inputValue.length).includes(inputValue.toLowerCase())
		);

		if (filterData.length > 0) {
			data = filterData;
		} else {
			alert('drink Not Found');
		}

		inputValue = '';
	};
</script>

<header class="flex justify-between px-8 py-4 bg-slate-700 text-white">
	<div class="italic text-lg font-semibold text-emerald-500">SampleApp</div>
	<div class="search-bar flex cursor-pointer">
		<input
			bind:value={inputValue}
			class="mr-0 width-[40px] outline-none pl-2 rounded-l rounded-bl sm:w-[250px] md:w-[300px] lg:w-[350px] bg-slate-500"
			type="text"
			name="search-cocktail"
			placeholder="search"
		/>
		<button class="px-3 py-1 text-sm rounded-r rounded-br bg-sky-800" on:click={searchData}>
			<Icon icon="iconamoon:search-duotone" width="20" height="20" />
		</button>
	</div>
	<div class="bar cursor-pointer" on:click={visibleSideBar} on:keydown={enterKeyPressed}>
		{#if sidebarActive}
			<Icon icon="mdi:cancel-bold" width="30" height="30" />
		{:else}
			<Icon icon="fe:bar" width="40" height="30" />
		{/if}
	</div>
</header>
