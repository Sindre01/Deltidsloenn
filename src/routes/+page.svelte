<script>
    import {theme} from "$lib/store/store"
    
</script>

<svelte:head>
	<title>Enklere lønn</title>
	<meta name="Din lønnshjelp" content="" />
</svelte:head>

<div class = "main">
    <img src="hvit-navn-logo.png" alt="logo">
    <!-- {#if $theme == "light"}
        <img src="svart-navn-logo.png" alt="logo">
    {:else}
        <img src="hvit-navn-logo.png" alt="logo">
    {/if} -->
</div>

<style>
    .main{
        display: flex;
        align-items: center;
        justify-content: center;
    }
    img{
        width: calc(40vh);
        height: calc(40vh);
    }
</style>
