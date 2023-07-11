<script>
        import { onMount } from 'svelte';
        import { navigate } from 'svelte-routing';
        //test
        export let selectCocktail;
        let cocktails = [];
        let searchstr = "";

        onMount(async () => {
                const response = await fetch('https://www.thecocktaildb.com/api/json/v1/1/list.php?c=list');
                const data = await response.json();
                cocktails = data.drinks || [];
        });

        function handleClick(cocktail) {
                selectCocktail(cocktail);
                navigate(`/cocktail/${cocktail.strCategory}`);
        }

        function handleKeyDown(event, cocktail) {
                if (event.key === 'Enter') {
                        handleClick(cocktail);
                }
        }
</script>

<main>
 
        <div class="topnav">
                <a class="navbutton" href={`/`}>
                        <div class="header-item" role="button" tabindex="0">
                                <p>Home</p>
                        </div>
                </a>

                <a class="navbutton" href={`/random/`}>
                        <div class="header-item" role="button" tabindex="0">
                                <p>Random Drink</p>
                        </div>
                </a>

                <a class="navbutton" href={`/filter/`}>
                        <div class="header-item" role="button" tabindex="0">
                                <p>Kategorien</p>
                        </div>
                </a>

                <a
                        class="navbutton floatright navbuttonleft"
                        href={`/search/${searchstr}`}
                >
                        <div class="header-item" role="button" tabindex="0">
                                <h3>Suchen</h3>
                        </div>
                </a>

                
                <input class="searchfield floatright" bind:value={searchstr} />
                
        </div>

        <h2>Category</h2>
        {#if cocktails.length > 0}
                <ul>
                        {#each cocktails as cocktail}
                                <a href={`/cocktail/${cocktail.strCategory}`}>
                                        <div class="cocktail-item" role="button" tabindex="0">
                                                <h3>{cocktail.strCategory}</h3>
                                        </div>
                                </a>
                        {/each}
                </ul>
        {:else}
                <p>Loading...</p>
        {/if}
</main>

<style>
        main {
                text-align: center;
        }

        ul {
                list-style-type: none;
                padding: 0;
        }

        li {
                cursor: pointer;
                padding: 8px;
                margin-bottom: 4px;
                background-color: #f0f0f0;
                border-radius: 4px;
        }

        li:focus {
                outline: none;
                background-color: #ddd;
        }

        .cocktail-item {
                width: 20%;
                height: 20%;
        }
</style>
