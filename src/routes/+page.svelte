<script>
        import { onMount } from "svelte";
        import { navigate } from "svelte-routing";
        //test
        export let selectCocktail;
        let cocktails = [];
        let searchstr = "";

        onMount(async () => {
                const response = await fetch(
                        "https://www.thecocktaildb.com/api/json/v1/1/search.php?f=d"
                );
                const data = await response.json();
                cocktails = data.drinks || [];
        });

        function handleClick(cocktail) {
                selectCocktail(cocktail);
                navigate(`/details/${cocktail.idDrink}`);
        }

        function handleKeyDown(event, cocktail) {
                if (event.key === "Enter") {
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

        {#if cocktails.length > 0}
                <ul>
                        {#each cocktails as cocktail}
                                <a href={`/details/${cocktail.idDrink}`}>
                                        <div
                                                class="cocktail-item"
                                                role="button"
                                                tabindex="0"
                                        >
                                                <h3>{cocktail.strDrink}</h3>

                                                <p>{cocktail.strAlcoholic}</p>
                                                <img
                                                        class="thumb"
                                                        src={cocktail.strDrinkThumb}
                                                        alt={cocktail.strDrink}
                                                />
                                        </div>
                                </a>
                        {/each}
                </ul>
        {:else}
                <p>Loading...</p>
        {/if}
</main>

<style>

        
</style>
