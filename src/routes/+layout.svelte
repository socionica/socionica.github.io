<script lang="ts">
    import "$lib/main.css";
    import { onMount, tick } from "svelte";
	import Title from "$lib/components/Title.svelte";
    import Header from "$lib/components/Header.svelte";
	import Footer from "$lib/components/Footer.svelte";
    import Loading from "$lib/components/Loading.svelte";

    let theme: 'dark' | 'light' | null;
    let complete = false;

    onMount(() => {
        theme = localStorage.getItem('theme') as 'dark' | 'light' | null;
        
        theme ? theme : window.matchMedia("(prefers-color-scheme: dark)").matches ? theme = 'dark' : theme = 'light';

        complete = true;
    });
</script>

<Title title/>

<div id="root" class={theme}>
    {#if complete}
        <Header bind:theme/>
            <slot/>
        <Footer/>
    {:else}
        <Loading/>
    {/if}
</div>

<style>
    #root {
        background-color: var(--background-pri);
        color: var(--text-color);
        font-family: 'Segoe UI', 'Roboto', sans-serif;
    }

    @media (max-width: 968px) {
        #root {
            overflow-x: hidden;
        }
    }
</style>