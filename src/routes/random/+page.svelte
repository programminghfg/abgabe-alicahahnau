<script>
        import { onMount } from "svelte";
        import { navigate } from "svelte-routing";
        //test
        export let selectCocktail;
        let cocktails = [];
        let searchstr = "";

        onMount(async () => {
                const response = await fetch(
                        "https://www.thecocktaildb.com/api/json/v1/1/random.php"
                );
                const data = await response.json();
                cocktails = data.drinks || [];
        });

        function handleClick(cocktail) {
                selectCocktail(cocktail);
                navigate(`/cocktail/${cocktail.strCategory}`);
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

        <h1 style="margin-left:60px">Dein random Drink</h1>
        {#if cocktails.length > 0}
                <ul>
                        {#each cocktails as cocktail}
                <div class="cocktail-details">
                        <h3>{cocktail.strDrink}</h3>
                        <img
                                class="thumb"
                                src={cocktail.strDrinkThumb}
                                alt={cocktail.strDrink}
                        />

                        <button type="button" class="collapsible"
                                >Zutaten</button
                        >
                        <div class="content">
                                {#if cocktail.strIngredient1 != null}
                                        <p>{cocktail.strIngredient1}</p>
                                {/if}
                                {#if cocktail.strIngredient2 != null}
                                        <p>{cocktail.strIngredient2}</p>
                                {/if}
                                {#if cocktail.strIngredient3 != null}
                                        <p>{cocktail.strIngredient3}</p>
                                {/if}
                                {#if cocktail.strIngredient4 != null}
                                        <p>{cocktail.strIngredient4}</p>
                                {/if}
                                {#if cocktail.strIngredient5 != null}
                                        <p>{cocktail.strIngredient5}</p>
                                {/if}
                                {#if cocktail.strIngredient6 != null}
                                        <p>{cocktail.strIngredient6}</p>
                                {/if}
                                {#if cocktail.strIngredient7 != null}
                                        <p>{cocktail.strIngredient7}</p>
                                {/if}
                                {#if cocktail.strIngredient8 != null}
                                        <p>{cocktail.strIngredient8}</p>
                                {/if}
                                {#if cocktail.strIngredient9 != null}
                                        <p>{cocktail.strIngredient9}</p>
                                {/if}
                                {#if cocktail.strIngredient10 != null}
                                        <p>{cocktail.strIngredient10}</p>
                                {/if}
                                {#if cocktail.strIngredient11 != null}
                                        <p>{cocktail.strIngredient11}</p>
                                {/if}
                                {#if cocktail.strIngredient12 != null}
                                        <p>{cocktail.strIngredient12}</p>
                                {/if}
                                {#if cocktail.strIngredient13 != null}
                                        <p>{cocktail.strIngredient13}</p>
                                {/if}
                                {#if cocktail.strIngredient14 != null}
                                        <p>{cocktail.strIngredient14}</p>
                                {/if}
                                {#if cocktail.strIngredient15 != null}
                                        <p>{cocktail.strIngredient15}</p>
                                {/if}
                        </div>
                        <button type="button" class="collapsible"
                                >Zubereitung</button
                        >
                        <div class="content">
                                {#if cocktail.strInstructions != null}
                                        <p>{cocktail.strInstructions}</p>
                                {/if}
                        </div>
                        <button type="button" class="collapsible">Infos</button>
                        <div class="content">
                                <p>{cocktail.strCategory}</p>
                                <p>{cocktail.strAlcoholic}</p>
                                <p>{cocktail.strGlass}</p>
                        </div>

                        <script>
                                var coll =
                                        document.getElementsByClassName(
                                                "collapsible"
                                        );
                                var i;

                                for (i = 0; i < coll.length; i++) {
                                        coll[i].addEventListener(
                                                "click",
                                                function () {
                                                        this.classList.toggle(
                                                                "active"
                                                        );
                                                        var content =
                                                                this
                                                                        .nextElementSibling;
                                                        if (
                                                                content.style
                                                                        .display ===
                                                                "block"
                                                        ) {
                                                                content.style.display =
                                                                        "none";
                                                        } else {
                                                                content.style.display =
                                                                        "block";
                                                        }
                                                }
                                        );
                                }
                        </script>
                        </div>
                {/each}
                </ul>
        {:else}
                <p>Loading...</p>
        {/if}
</main>

<style>
        .thumb {
                width: 200px;
        }
</style>
