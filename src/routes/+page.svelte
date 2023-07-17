<script>
	import FrontPage from '../Component/FrontPage.svelte';
	import Header from '../Component/Header.svelte';
	import Sidebar from '../Component/Sidebar.svelte';
	import AddItem from '../Component/AddItem.svelte';
	import { onMount } from 'svelte';

	let sidebarActive = false;
	let loading = false;
	let errorHappened = false;
	let data = null;
	let addItemActive = false;
	let addedData = [];

	onMount(() => {
		console.log(addedData);
		console.log('hello');
		const storedData = sessionStorage.getItem('myArray');
		if (storedData) {
			data = JSON.parse(storedData);
		}
	});
</script>

<Header bind:sidebarActive bind:data />
<Sidebar
	bind:sidebarActive
	bind:data
	bind:loading
	bind:errorHappened
	bind:addItemActive
	bind:addedData
/>
<FrontPage bind:data bind:loading bind:errorHappened />
{#if addItemActive}
	<AddItem bind:data bind:addedData bind:addItemActive />
{/if}
