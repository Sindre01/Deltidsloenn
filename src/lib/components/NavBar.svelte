<script>
    import { onMount } from "svelte";
    import {theme} from "$lib/store/store.js"
	import IconButton from "@smui/icon-button";
    
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

<div class="navBar">
    <a href = "/">Hjem</a>
	<a href = "/kalkulator">Kalkulator</a>
	<a href="/about">about</a>
	<IconButton style = "color: yellow;"on:click={()=>toggleTheme()}> 
        {#if $theme == "light"}
            <span class="material-icons">dark_mode</span>
        {:else}
            <span class="material-icons">light_mode</span>
        {/if}
    </IconButton>

</div>
<style>
.navBar{
    display: flex;
    align-items: center;
    justify-content: right;
}
a{ 
    margin-right: 10px
}
</style>