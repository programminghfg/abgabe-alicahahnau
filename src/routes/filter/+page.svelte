<script>
    import { page } from '$app/stores';
    import { onMount } from 'svelte';
    let cocktailId = 0;
    let cocktails = [];
    let url;
    let searchstr = "";

    onMount(async () => {
            cocktailId = $page.params.id;
            url = `https://www.thecocktaildb.com/api/json/v1/1/list.php?c=list`
            const response = await fetch(url);
            const data = await response.json();
            cocktails = data.drinks || [];
    });

    function handleClick(cocktail) {
            selectCocktail(cocktail);
            navigate(`/cocktail/${cocktail.idDrink}`);
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
                        <p>Suchen</p>
                </div>
        </a>

        
        <input class="searchfield floatright" bind:value={searchstr} />
        
</div>


<h1 style="margin-left:60px">Kategorien</h1>
{#if cocktails.length > 0}
    <ul>
            {#each cocktails as cocktail}
                    <a href={`/cocktail/${cocktail.strCategory}`}>
                            <div class="cocktail-cat" role="button" tabindex="0">
                                    <h3>{cocktail.strCategory}</h3>
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
