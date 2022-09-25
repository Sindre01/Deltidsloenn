<script>
	import Form from "$lib/components/Form.svelte";
</script>

<svelte:head>
	<title>Home</title>
	<meta name="description" content="Svelte demo app" />
</svelte:head>

<section>
	<h1>
		UB-Kalkulator
	</h1>

	<h2>
		Regner ut lønn inkludert kveldstillegg
	</h2>
	<Form/>

</section>

<style>
	section {
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: center;
		flex: 1;
	}

	h1 {
		width: 100%;
		font-style: italic;
	}


</style>
