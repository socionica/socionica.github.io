<script lang="ts">
    import { tick } from "svelte";
    import { afterNavigate } from "$app/navigation";
    import { pages } from "$lib/main.svelte"
    
    export let header = false;
    export let sidebar = false;

    let paths = Array.from(pages.keys());
    let root_paths = paths.filter(p => p.split('/').length === 3);
    let local_paths: string[] = [];
    
    const expandList = (e: MouseEvent & { currentTarget: EventTarget & HTMLUListElement } | KeyboardEvent & { currentTarget: EventTarget & HTMLUListElement }) => {
        const list = e.currentTarget;
        list.classList.toggle('open');
    }

    const parsePath = (path: string, module: 'root' | 'parent' | 'parents' | 'children' | 'direct children'): string | string[] => {
        switch (module) {
            case "root":
                const root = '/' + path.split('/')[1] + '/';
                return root;
            case "parent":
                const parent = paths.find(p => p == path.slice(0, path.lastIndexOf('/', path.lastIndexOf('/') -1) + 1)) || '/';
                return parent;
            case "parents":
                const parents: string[] = [];
                for (let i = 0; i < path.split('/')!.length - 2; i++) {
                    path = parsePath(path, 'parent') as string;
                    parents.push(paths.find(p => p == path)!);
                }
                return parents;
            case "children":
                const children = paths.filter(p => p != path && p.startsWith(path));
                return children;
            case "direct children":
                const _children = parsePath(path, 'children') as string[];
                const direct_children = _children.filter(p => parsePath(p, 'parent') === path);
                return direct_children;
        }
    }

    const updateNavigation = () => {
        let path = window.location.pathname;
        let nav_items = document.querySelectorAll('.nav-item');
        let nav_lists = document.querySelectorAll('.nav-list');

        console.log('executou', nav_lists)
        console.log('executou', path)

        local_paths = paths.filter(p => p != parsePath(path, 'root') && p.startsWith(parsePath(path, 'root') as string));

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

            l.id == path ? l.classList.add('active') : l.classList.remove('active');
            l.id == path || parsePath(path, 'parent').includes(l.id) ? l.classList.add('open') : l.classList.remove('open');
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
        <li id={path} class="nav-item">
            <a href={path}>{pages.get(path)}</a>
        </li>
    {/each}
{:else if sidebar}
    <!-- Local paths -->
    {#each local_paths as path}
        <!-- svelte-ignore a11y-click-events-have-key-events -->
        <ul id={path} class="nav-list" on:click|self={(e) => expandList(e)} on:keypress|self={(e) => expandList(e)}>
            <a href={path} on:click={(e) => {
                e.currentTarget.scrollIntoView({ behavior: "smooth", block: "center" });
            }}>{pages.get(path)}</a>
        </ul>
    {/each}
{:else}
    <!-- All paths -->
    {#each paths as path}
        <ul id={path} class="nav-list">
            <a href={path}>{pages.get(path)}</a>
        </ul>
    {/each}
{/if}

{#if false}
    <dummy class="nav-item nav-list open active"><ul><a href="/">dummy</a></ul></dummy>
{/if}

<style>
    .nav-item {
        width: 100%;
        margin: 0 1rem;

        display: flex;
        place-content: center;
        place-items: center;
    }

        .nav-item a {
            color: var(--text-color);
            font-weight: 600;
            text-decoration: none;
        }

        .nav-item.open {
            border-bottom: 2px solid var(--text-color); /* OLHAR */
            padding-top: 2px;
        }

            .nav-item.open a {
                color: var(--title-color);
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

            .nav-list a:hover,
            .nav-list.active a {
                color: var(--title-color);
            }
        
        .nav-list ul {
            display: none;
        }

        .nav-list.open ul {
            display: block;
        }

</style>