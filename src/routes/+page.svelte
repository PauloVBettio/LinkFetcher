<script>
	import './app.css';
	import { JsonView } from '@zerodevx/svelte-json-view'

	let link = '';
	let isLoading = false;
	let responseData = null;

	const handleSubmit = async () => {
		isLoading = true;
		try {
			const response = await fetch(link);
			const data = await response.json();
			responseData = data;
		} catch (error) {
			console.error('Error fetching data:', error);
		} finally {
			isLoading = false;
		}
	};
</script>

<head>
	<title>Teste de fetch</title>
</head>

<style lang="postcss">
    :global(html) {
        background-color: theme(colors.zinc.900);
        color: theme(colors.zinc.100);
    }
</style>

<body class="container mx-auto max-w-7xl mt-8 font-mono rounded-xl border-r border-t border-zinc-500 bg-black p-8">
<h1 class="text-2xl font-bold">Fetch Tester</h1>
<input class="bg-zinc-900 border-green-500 rounded-md" bind:value={link} placeholder="Link" type="text" name="address"
			 id="address">
<button on:click={handleSubmit} class="bg-green-500 rounded-md p-2 text-black font-black" disabled={isLoading}>{isLoading ? 'Loading...' : 'Fetch Data'}</button>
{#if responseData}
	<div>
		<h2>Data Fetched:</h2>
		<JsonView json={responseData}></JsonView>
	</div>
{/if}
</body>