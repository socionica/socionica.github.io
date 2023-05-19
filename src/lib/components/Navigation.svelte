<script lang="ts">
    import { tick } from "svelte";
    import { afterNavigate } from "$app/navigation";
    import { pages, parsePath } from "$lib/main.svelte"
    
    export let header = false;
    export let sidebar = false;

    let paths = Array.from(pages.keys());
    let root_paths = paths.filter(p => p.split('/').length === 3);
    let local_paths: string[] = [];
    
    const expandList = (e: MouseEvent & { currentTarget: EventTarget & HTMLUListElement } | KeyboardEvent & { currentTarget: EventTarget & HTMLUListElement }) => {
        const list = e.currentTarget;
        list.classList.toggle('open');
    }

    const updateNavigation = () => {
        let path = window.location.pathname;
        let nav_items = document.querySelectorAll('.header-nav-item');
        let sidebar_nav_items = document.querySelectorAll('.sidebar-nav-item');
        let menu_nav_items = document.querySelectorAll('.menu-nav-item');

        local_paths = parsePath(path, 'local') as string[];

        nav_items.forEach(i => {
            i.id == parsePath(path, 'root') ? i.classList.add('open') : i.classList.remove('open');
        });

        sidebar_nav_items.forEach(l => {
            const direct_children = parsePath(l.id, 'direct children') as string[];
            if (direct_children) {
                sidebar_nav_items.forEach(_l => {
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

        menu_nav_items.forEach(l => {
            const direct_children = parsePath(l.id, 'direct children') as string[];
            if (direct_children) {
                menu_nav_items.forEach(_l => {
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
    
    afterNavigate(async () => {
        updateNavigation();

        await tick(); // Ainda quero resolver isso alternativamente!!!
        updateNavigation();
    });
</script>

{#if header}
    <!-- Root paths -->
    {#each root_paths as path}
        <li id={path} class="header-nav-item">
            <a href={path}>{pages.get(path)}</a>
        </li>
    {/each}
{:else if sidebar}
    <!-- Local paths -->
    {#each local_paths as path}
        <!-- svelte-ignore a11y-click-events-have-key-events -->
        <ul id={path} class="sidebar-nav-item nav-list" on:click|self={(e) => expandList(e)} on:keypress|self={(e) => expandList(e)}>
            <a href={path}>{pages.get(path)}</a>
        </ul>
    {/each}
{:else}
    <!-- All paths -->
    {#each paths as path}
        <ul id={path} class="menu-nav-item nav-list" on:click|self={(e) => expandList(e)} on:keypress|self={(e) => expandList(e)}>
            <a href={path}>{pages.get(path)}</a>
        </ul>
    {/each}
{/if}

{#if false}
    <dummy class="header-nav-item sidebar-nav-list menu-nav-list nav-list open active"><ul></ul><a href="/">dummy</a></dummy>
{/if}

<style>
    .header-nav-item {
        width: 100%;
        margin: 0 1rem;

        display: flex;
        place-content: center;
        place-items: center;
    }

        .header-nav-item a {
            color: var(--text-color);
            font-weight: 600;
            text-decoration: none;
        }

    .header-nav-item.open {
        border-bottom: 2px solid var(--text-color);
        padding-top: 2px;
    }

        .header-nav-item.open>a {
            color: var(--title-color);
            font-weight: 700;
        }

    .nav-list {
        background-color: hsla(0, 0%, 40%, 8%);
        border-radius: 5px 0 0 3px;
        margin: .5rem 0;
        padding: .5rem;
    }

        .nav-list a {
            color: var(--text-color);
            text-decoration: none;
        }
        
        .nav-list>ul {
            display: none;
        }

        .nav-list.open>ul {
            display: block;
        }
</style>