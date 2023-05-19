<script lang="ts">
    import { afterNavigate } from "$app/navigation";
    import { pages, parsePath } from "$lib/main.svelte";

    export let top = false;
    export let side = false;

    const expandList = (e: MouseEvent & { currentTarget: EventTarget & HTMLUListElement } | KeyboardEvent & { currentTarget: EventTarget & HTMLUListElement }) => {
        const list = e.currentTarget;
        list.classList.toggle('open');
    }

    const updateNavigation = () => {
        let path = window.location.pathname;
        let nav_items = document.querySelectorAll('.nav-item');
        let nav_lists = document.querySelectorAll('.nav-list');

        nav_items.forEach(i => {
            i.id == parsePath(path, 'root') ? i.classList.add('open') : i.classList.remove('open');
        });

        nav_lists.forEach(l => {
            const direct_children = parsePath(l.id, 'direct children') as string[];
            if (direct_children) {
                nav_lists.forEach(_l => {
                    direct_children.includes(_l.id) ? l.appendChild(_l) : null;
                })
            }

            l.classList.remove('open', 'active');
            if (l.id == path) {
                l.classList.add('open', 'active');
                l.scrollIntoView({ behavior: "smooth", block: "center" });
            } else if (parsePath(path, 'parent').includes(l.id)) {
                l.classList.add('open')
            }
        });
    }

    afterNavigate(() => {

    });
</script>

{#if top}
    {#each parsePath('/', 'roots') as path}
    <li id={path} class="header-nav-item">
        <a href={path}>{pages.get(path)}</a>
    </li>
    {/each}
{:else if side}
    {#each Array.from(pages.keys()) as path}
        <ul id={path} class="menu-nav-list" on:click|self={(e) => expandList(e)} on:keypress|self={(e) => expandList(e)}>
            <a href={path}>{pages.get(path)}</a>
        </ul>
    {/each}
{/if}

<style>

</style>