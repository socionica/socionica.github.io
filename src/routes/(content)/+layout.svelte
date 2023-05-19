<script lang="ts">
    import Navigation from "$lib/components/Navigation.svelte";
    import Title from "$lib/components/Title.svelte";
    import Aside from "$lib/components/Aside.svelte";
</script>

<main>
    <div class="sidebar">
        <div class="sidebar-nav">
            <Navigation sidebar/>
        </div>
    </div>
    <div class='content'>
        <div class="title-container">
            <h1><Title text/></h1>
            <a class="source" href="/">FONTES</a>
        </div>
        <div class="article-container">
            <article>
                <slot/>
            </article>
            <aside>
                <Aside/>
            </aside>
        </div>
    </div>
</main>

<style>
    main {
        display: grid;
        grid-template-columns: 1fr 4fr;
    }

    .sidebar {
        grid-column: 1;

        background-color: var(--background-sec);
        height: 100vh;
        position: sticky;
        top: 0;
    }

        .sidebar-nav {
            height: calc(100vh - 4rem);
            overflow-y: scroll;
        }

    .content {
        grid-column: 2;

        margin: 0 1rem;
    }

        .title-container {
            border-bottom: 1px solid var(--text-color);
            padding: 1rem 0;

            display: flex;
            place-content: space-between;
        }

            .source {
                color: var(--text-color);
                font-family: monospace;
                text-decoration: none;

                border: 1px dashed var(--text-color);
                border-radius: 2px;
                margin: auto 2rem;
                padding: 0.25rem;
                
                align-self: center;
            }

                .source:hover,
                .source:focus {
                    background-color: var(--background-ter);
                }

        .article-container {
            display: grid;
            grid-template-columns: 3fr 1fr;
            grid-column-gap: 1rem;
        }

            article {
                grid-column: 1;
            }

            aside {
                grid-column: 2;
            }

    @media (max-width: 968px) {
        main {
            display: block;
        }

        .sidebar {
            display: none;
        }

        .article-container {
            display: block;
        }
        
        aside {
            display: none;
        }
    }
</style>