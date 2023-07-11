<script>
        import { page } from '$app/stores';
        import { onMount } from 'svelte';
        let cocktailId = 0;
        let cocktails = [];
        let url;
        let searchstr = "";

        onMount(async () => {
                cocktailId = $page.params.id;
                url = `https://www.thecocktaildb.com/api/json/v1/1/search.php?s=${cocktailId}`
                const response = await fetch(url);
                const data = await response.json();
                cocktails = data.drinks || [];
        });

        function handleClick(cocktail) {
                selectCocktail(cocktail);
                navigate(`/details/${cocktail.idDrink}`);
        }

        function handleKeyDown(event, cocktail) {
                if (event.key === 'Enter') {
                        handleClick(cocktail);
                }
        }

</script>
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

<h1>Suchen: {cocktailId}</h1>
{#if cocktails.length > 0}
        <ul>
                {#each cocktails as cocktail}
                        <a href={`/details/${cocktail.idDrink}`}>
                                <div class="cocktail-item" role="button" tabindex="0">
                                        <h3>{cocktail.strDrink}</h3>
                                        <img class="thumb" src={cocktail.strDrinkThumb} alt={cocktail.strDrink} />
                                </div>
                        </a>
                {/each}
        </ul>
{:else}
<p>Loading...</p>
<p>{cocktails.length}</p>
{/if}
<style>

        .thumb {
                width: 50px;
        }

</style>
