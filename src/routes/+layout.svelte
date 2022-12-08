<script>
	
	// import '../app.css';
	
	import { theme } from "$lib/store/store.js";
	import { onMount } from "svelte";

	onMount(async () => {
			// Set up our MediaQueryList
		const prefersDarkMode = window.matchMedia('(prefers-color-scheme: dark)')
		// Initial theme config from current state
		$theme =  prefersDarkMode.matches ? 'dark' : 'light'

	})
  
	function toggleTheme(){
	  $theme = $theme === "light" ? "dark" : "light";
	}

</script>

<svelte:head>
	{#if $theme == "dark"}
		<link rel="stylesheet" href="src/theme/dark/_smui-theme.scss" />
	{:else if $theme == "light"}
		<link rel="stylesheet" href="src/theme/_smui-theme.scss" />
	{/if}
</svelte:head>

<!-- <button on:click={()=>toggleTheme()}> {$theme}</button>
<a href="/about">about</a>
<a href = "/">Home</a> -->
<main>
	<slot />
</main>

<!-- <footer>
	<p>Laget av Sindre Erichsen</p>
</footer> -->

<style>
	main {
		flex: 1;
		display: flex;
		flex-direction: column;
		padding: 1rem;
		width: 100%;
		max-width: 1024px;
		margin: 0 auto;
		box-sizing: border-box;
	}

	/* footer {
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: center;
		padding: 40px;
	}

	footer a {
		font-weight: bold;
	}

	@media (min-width: 480px) {
		footer {
			padding: 40px 0;
		}
	} */
</style>
