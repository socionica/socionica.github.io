<script lang="ts">
	import Navigation from "$lib/components/Navigation.svelte";

    export let theme: string | null;

    const changeTheme = () => {
        theme == 'dark' ? theme = 'light' : theme = 'dark';
        localStorage.setItem('theme', theme);
    };

    const toggleMenu = () => {
        const menu = document.querySelector('.menu') as HTMLElement;
        const header = document.querySelector('header') as HTMLElement;
    
        menu.style.width ? menu.style.width : menu.style.width = '0%'
        
        if (menu.style.width == '0%') {
            menu.style.width = 'calc(100% - 3.75rem)';
            header.style.transform = 'translateX(calc(100% - 3.75rem))'
        } else {
            menu.style.width = '0%';
            header.style.transform = 'translateX(0)'
        }
    }
</script>

<div class="menu">
    <div class="menu-head">
        <h2>Central Sociônica</h2>
        <button class="change-theme-btn" on:click={changeTheme}>
            <svg
            viewBox="0 0 190.5 190.49999"
            version="1.1"
            class={theme}
            xmlns="http://www.w3.org/2000/svg">
                <path
                id="path17429"
                style="fill:#848484;fill-opacity:0;stroke:currentcolor;stroke-width:26.4354;stroke-linecap:round;stroke-linejoin:bevel;stroke-opacity:1"
                d="m 153.31432,153.31432 a 82.115347,82.115347 0 0 1 -116.128638,0 82.115347,82.115347 0 0 1 -3e-6,-116.12864 82.115347,82.115347 0 0 1 116.128641,0 82.115347,82.115347 0 0 1 0,116.12864 z" />
                <path
                style="fill:currentcolor;fill-opacity:1;stroke:none;stroke-width:26.4354;stroke-linecap:round;stroke-linejoin:bevel;stroke-dasharray:none;stroke-opacity:1"
                d="M 37.185685,153.31432 153.31432,37.185682 c 0,0 58.06432,78.942948 0,116.128638 -58.064317,37.18568 -116.128635,0 -116.128635,0 z"
                id="path17486" />
            </svg>
        </button>
    </div>
    <nav class="menu-nav">
        <Navigation/>
    </nav>
</div>
<header>
    <div class="toggle-menu">
        <button class="toggle-menu-btn" on:click={toggleMenu}>
            <div class="line"/>
            <div class="line"/>
            <div class="line"/>
        </button>
    </div>  
    <div class="logo-container">
        <a class="header-logo" href="/">
            <svg
            viewBox="0 0 190.5 190.49999"
            version="1.1"
            xmlns="http://www.w3.org/2000/svg">
                <g
                id="g2190"
                transform="matrix(1.595163,0,0,1.595163,-34.424625,-26.066128)"
                style="display:inline">
                    <path
                    id="path2170"
                    style="fill:#8fcaf9;fill-opacity:1;stroke:currentcolor;stroke-width:6.34982;stroke-linejoin:round;stroke-dasharray:none;stroke-opacity:1"
                    d="M 135.56171,52.9527 123.30032,41.534428 105.78406,25.222617 v 0 l -41.983996,9.962629 47.293946,44.04188 c 2.91121,2.71102 7.4374,2.549866 10.14841,-0.361335 l 14.68063,-15.76464 c 2.71103,-2.911216 2.54986,-7.437402 -0.36133,-10.148422 z" />
                    <path
                    id="path2172"
                    style="fill:#fff59c;fill-opacity:1;stroke:currentcolor;stroke-width:6.34982;stroke-linejoin:round;stroke-dasharray:none;stroke-opacity:1"
                    d="m 27.023095,99.056428 12.261391,11.418272 17.51627,16.31181 v 0 L 98.784743,116.82388 51.490792,72.782 c -2.911193,-2.711025 -7.4374,-2.549864 -10.148423,0.36134 L 26.661738,88.90798 c -2.711023,2.911203 -2.549852,7.437407 0.36135,10.148418 z" />
                    <path
                    id="path2178"
                    style="fill:#a5d7a7;fill-opacity:1;stroke:currentcolor;stroke-width:6.34982;stroke-linejoin:round;stroke-dasharray:none;stroke-opacity:1"
                    d="M 132.11352,98.801266 119.85214,87.383003 102.33586,71.071198 v 0 l -41.983977,9.962596 47.293937,44.041886 c 2.91119,2.71102 7.43738,2.54986 10.14842,-0.36135 l 14.68062,-15.76464 c 2.71102,-2.91121 2.54988,-7.4374 -0.36134,-10.148424 z" />
                    <path
                    id="path2180"
                    style="fill:#f9a09a;fill-opacity:1;stroke:currentcolor;stroke-width:6.34982;stroke-linejoin:round;stroke-dasharray:none;stroke-opacity:1"
                    d="m 30.574217,53.303738 12.261389,11.418257 17.516279,16.311814 v 0 L 102.33586,71.071184 55.041922,27.029306 C 52.130718,24.318284 47.604523,24.479442 44.893501,27.390645 L 30.212872,43.155296 c -2.711016,2.911191 -2.549864,7.437399 0.36134,10.148422 z" />
                </g>
            </svg>
        </a>
    </div>
    <div class="navigation-container">
        <nav class="header-nav">
            <Navigation header/>
        </nav>
        <button class="change-theme-btn" on:click={changeTheme}>
            <svg
            viewBox="0 0 190.5 190.49999"
            version="1.1"
            class={theme}
            xmlns="http://www.w3.org/2000/svg">
                <path
                id="path17429"
                style="fill:#848484;fill-opacity:0;stroke:currentcolor;stroke-width:26.4354;stroke-linecap:round;stroke-linejoin:bevel;stroke-opacity:1"
                d="m 153.31432,153.31432 a 82.115347,82.115347 0 0 1 -116.128638,0 82.115347,82.115347 0 0 1 -3e-6,-116.12864 82.115347,82.115347 0 0 1 116.128641,0 82.115347,82.115347 0 0 1 0,116.12864 z" />
                <path
                style="fill:currentcolor;fill-opacity:1;stroke:none;stroke-width:26.4354;stroke-linecap:round;stroke-linejoin:bevel;stroke-dasharray:none;stroke-opacity:1"
                d="M 37.185685,153.31432 153.31432,37.185682 c 0,0 58.06432,78.942948 0,116.128638 -58.064317,37.18568 -116.128635,0 -116.128635,0 z"
                id="path17486" />
            </svg>
        </button>
    </div>
</header>

<style>
    header {
        background-color: var(--background-ter);
        height: 4rem;

        display: grid;
        grid-template-columns: 1fr 1fr 3fr;
    }

    .logo-container {
        grid-column: 1;

        display: flex;
        place-content: center;
    }

        .header-logo svg {
            color: var(--svg-color);
            height: 4rem;
            opacity: .75;
            transition: opacity 0.2s ease-in-out;
        }
        
            .header-logo svg:hover {
                opacity: 1;
            }

    .navigation-container {
        grid-column: 3;
        height: inherit;

        display: flex;
    }

        .header-nav {
            flex: 1;

            display: flex;
            place-content: space-around;
        }

        .change-theme-btn {
            background: none;
            border: none;
            color: none;

            margin: 1rem;
        }

        .change-theme-btn svg {
            color: var(--svg-color);
            height: 2rem;
            transition: transform 0.2s ease-in-out;
        }

            .change-theme-btn svg.dark {
                transform: rotateZ(0deg);
            }

            .change-theme-btn svg.light {
                transform: rotateZ(180deg);
            }
    
    .menu {
        display: none;
        width: 0;
    }

        .toggle-menu-btn {
            display: none;
        }
    
    @media (max-width: 968px) {
        .menu {
            display: block;
            position: fixed;
            top: 0;
            bottom: 0;
            left: 0;

            background-color: var(--background-sec);
            z-index: 1;

            transition: transform .1s ease;
        }

            .menu-head {
                height: 4rem;
                overflow: hidden;

                display: flex;
                place-content: center;
                place-items: center;
            }

                .change-theme-btn {
                    margin-right: 0;
                }

            .menu-nav {
                height: calc(100% - 4rem);
                overflow-y: scroll;
            }

        header {
            display: flex;
            place-content: space-between;
            
            transition: transform .1s ease;
        }

            .toggle-menu {
                background-color: var(--background-sec);
                border-radius: 0 1rem 1rem 0;
                height: 3.5rem;
                width: 3.5rem;
                margin: .25rem 0;
                padding: 1rem;
                padding-left: .75rem;

                display: block;
            }

                .toggle-menu-btn {
                    background: none;
                    border: none;
                    height: 100%;
                    width: 100%;

                    display: flex;
                    flex-flow: column;
                    place-items: center;
                    place-content: space-around;
                }

                    .line {
                        background-color: var(--svg-color);
                        border-radius: 3px;
                        height: 20%;
                        width: 100%;
                    }

            .header-logo {
                margin: 0 1rem;
            }
                
        .navigation-container {
            display: none;
        }
    }
</style>

