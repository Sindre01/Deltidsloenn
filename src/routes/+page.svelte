<script>
    import {theme} from "$lib/store/store"
    
</script>

<svelte:head>
	<title>Enklere lønn</title>
	<meta name="Din lønnshjelp" content="" />
</svelte:head>

<div class = "main">
    <!-- <img src="hvit-logo.png" alt="logo"> -->
        <!-- Down Arrow Animation
        <svg xmlns="http://www.w3.org/2000/svg" width="100" height="200" viewBox="0 0 100 200" class="arrow down">
            <path d="M50 100 L50 180" fill="transparent" stroke="white" stroke-width="2" id="downArrowPath" />
            <circle cx="50" cy="100" r="2" fill="white" id="downArrowCircle" />
        </svg> -->
    <div class = "title">
        <svg xmlns="http://www.w3.org/2000/svg" width="200" height="100" viewBox="0 0 200 100" class="arrow left">
            <path d="M100 50 L20 50" fill="transparent" stroke="white" stroke-width="2" id="leftArrowPath" />
            <!-- <circle cx="100" cy="50" r="2" fill="white" id="leftArrowCircle" /> -->
        </svg>
        <h1>Enklere lønn</h1>
        <p>Lønn gjort enklere</p>
        <!-- Left Arrow Animation -->

        <!-- Right Arrow Animation -->
        <svg xmlns="http://www.w3.org/2000/svg" width="200" height="100" viewBox="0 0 200 100" class="arrow right">
            <path d="M100 50 L180 50" fill="transparent" stroke="white" stroke-width="2" id="rightArrowPath" />
            <!-- <circle cx="100" cy="50" r="2" fill="white" id="rightArrowCircle" /> -->
        </svg>
    

    </div>
     <!-- Up Arrow Animation
     <svg xmlns="http://www.w3.org/2000/svg" width="100" height="200" viewBox="0 0 100 200" class="arrow up">
        <path d="M50 100 L50 20" fill="transparent" stroke="white" stroke-width="2" id="upArrowPath" />
        <circle cx="50" cy="100" r="2" fill="white" id="upArrowCircle" />
    </svg> -->
    <!-- {#if $theme == "light"}
        <img src="svart-navn-logo.png" alt="logo">
    {:else}
        <img src="hvit-navn-logo.png" alt="logo">
    {/if} -->
    <!-- <svg xmlns="http://www.w3.org/2000/svg" width="100" height="100" viewBox="0 0 100 100" class="arrow">
        <path d="M50 5 L10 50 L50 5 L50 95 L90 50 L50 95" fill="transparent" stroke="white" stroke-width="2" />
    </svg> -->
</div>

<style>
    .main{
        margin-top: 20vh;
        display: flex;
        align-items: center;
        justify-content: center;
        /* background-color: aqua; */
        
    }
    .arrow {
        width: 100px;
        height: 100px;
        animation-duration: 6s;
        animation-timing-function: ease-in-out;
        animation-fill-mode: forwards;
    }

    .left {
        animation-name: moveLeftArrow;
    }

    .right {
        animation-name: moveRightArrow;
    }

    @keyframes moveLeftArrow {
        0% {
            transform: translate(0, 0);
        }
        100% {
            transform: translate(-100px, 0);
        }
    }

    @keyframes moveRightArrow {
        0% {
            transform: translate(0, 0);
        }
        100% {
            transform: translate(100px, 0);
        }
    }
    .up {
        animation-name: moveUpArrow;
    }

    .down {
        animation-name: moveDownArrow;
    }

    @keyframes moveUpArrow {
        0% {
            transform: translate(0, 0);
        }
        100% {
            transform: translate(0, -80px);
        }
    }

    @keyframes moveDownArrow {
        0% {
            transform: translate(0, 0);
        }
        100% {
            transform: translate(0, 80px);
        }
    }
    h1 {
        margin: 0px;
        font-size: 70px;
        font-weight: 600;
        /* background-image: linear-gradient(to left, #553c9a, #b393d3); */
        background-image: linear-gradient(to left, #007ea7, #00a8e8);
        color: transparent;
        background-clip: text;
        -webkit-background-clip: text;


    }
    p {
        font-style: italic;
    }
    .title {
        display: flex;
        flex-direction: column;
        align-items: center;
        justify-content: center;
        /* background-color: red; */
    }
    img{
        width: calc(40vh);
        height: calc(40vh);
        /* background-color: blue; */
    }
</style>
