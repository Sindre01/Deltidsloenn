<script>
    import { onMount } from "svelte";
    import {theme} from "$lib/store/store.js"
	import IconButton from "@smui/icon-button";
    import { fly } from 'svelte/transition';
    
    onMount(async () => {
        // Set up our MediaQueryList
    const prefersDarkMode = window.matchMedia('(prefers-color-scheme: dark)')
    // Initial theme config from current state
    $theme =  prefersDarkMode.matches ? 'dark' : 'light'

	})
  
	function toggleTheme(){
	  $theme = $theme === "light" ? "dark" : "light";
	}
    
    let show = false
    function clickOutside(node, { enabled: initialEnabled, cb }) {
    const handleOutsideClick = ({ target }) => {
      if (!node.contains(target)) {
        cb();
      }
    };

    function update({enabled}) {
      if (enabled) {
        window.addEventListener('click', handleOutsideClick);
      } else {
        window.removeEventListener('click', handleOutsideClick);
      }
    }

    update({ enabled: initialEnabled });
    return {
      update,
      destroy() {
        window.removeEventListener( 'click', handleOutsideClick );
      }
    };
  }

let current = 0;
/**
	 * @param {number} el
	 */
function setCurrent(el){
    current = el
    show = false;
}
</script>

<svelte:head>
	{#if $theme == "dark"}
		<link rel="stylesheet" href="src/theme/dark/_smui-theme.scss" />
	{:else if $theme == "light"}
		<link rel="stylesheet" href="src/theme/_smui-theme.scss" />
	{/if}
</svelte:head>

<div use:clickOutside={{ enabled: show, cb: () => show = false }} >
    <div class = "menu">
        <IconButton style = "color: white; position: fixed; left: 10px; top: 5px;  z-index: 2;" ripple={false} on:click={() => show = !show}> 
            <span  class="material-icons">menu</span>
        </IconButton>
        
        <!-- <IconButton> 
            <a href = "/">Deltidslønn</a>
        </IconButton> -->
    
        <IconButton style = "position: fixed; right: 10px; top: 5px;" ripple={false} on:click={()=>toggleTheme()}> 
            {#if $theme == "light"}
                <span class="material-icons">dark_mode</span>
            {:else}
                <span class="material-icons">light_mode</span>
            {/if}
        </IconButton>
    </div>



    {#if show}
    
        <div class="navBar" in:fly="{{ x: -200, duration: 200 }}" out:fly="{{ x: -200, duration: 200 }}">
            <ul>
                <li><a class:current={current === 0} on:click={()=>setCurrent(0)} href = "/">Hjem</a></li>
                <li><a class:current={current === 1}  on:click={()=>setCurrent(1)}  href = "/kalkulator">Kalkulator</a></li>
                <li> <a class:current={current === 2}   on:click={()=>setCurrent(2)} href="/about">about</a></li>
            </ul>
        </div>
    {/if}
 </div>

<style>
    .menu{
        color: white;
    }
    .current{
        position: relative;
    
    }
    .current::after {
        content: "";
        position: absolute;
        bottom: 0;
        left: 0;
        width: 100%;
        height: 2px;
        background-color: red;
        
    }
    /* .menu{
        display: flex;
        flex-direction: row;
        width: 100%;
        justify-content: center;
        position: fixed;
        
    } */
    .navBar{
        position: fixed;
        top:0;
        width: 100%;
        left: 0;
        padding-top: 5vh;
        padding-bottom: 5vh;
        /* height: 100%; */
        background-color: var(--primary-color);
        box-shadow: 0 30px 40px rgba(0,0,0,.1);
        z-index: 1;
   
    }
    ul {
        justify-content: space-between;
        display: flex;
        align-items: center;
        gap: 5vh;
        flex-direction: column;
        border:none;
        list-style: none;
        font-size:1.1rem;
    }
    a:hover{
        text-decoration: none;
    }
    a{ 
        border: none;
        color: white;
    }
</style>