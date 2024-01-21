<script>
  import { onMount } from 'svelte';
  import RecipeList from '../lib/RecipeList.svelte';
  import { fetchRecipes } from '../services';
  import { useParams } from 'svelte-navigator';
  import { fade } from 'svelte/transition';

  const params = useParams();

  let recipes = [];
  let isLoaded = false;
  let error = null;

  $: searchRecipes = recipes.filter((recipe) =>
    recipe.name.toLowerCase().includes($params.search.toLowerCase())
  );

  onMount(async () => {
    try {
      recipes = await fetchRecipes();
      console.log(recipes);
      isLoaded = true;
    } catch (e) {
      error = e;
    }
  });
</script>

<div>
  <h1>Recettes trouvées</h1>
  {#if !isLoaded}
    <span>Chargement des recettes...</span>
  {:else if error}
    <span>Impossible de charger les recettes du jour</span>
  {:else if searchRecipes.length === 0 && isLoaded}
    <span>Aucune recette trouvée pour cette recherche</span>
  {:else}
    <div in:fade={{ duration: 200 }}>
      <RecipeList recipes={searchRecipes} />
    </div>
  {/if}
</div>

<style>
  h1 {
    font-size: 24px;
    font-weight: 500;
  }

  div {
    display: flex;
    flex-direction: column;
    width: fit-content;
    margin: auto;
  }
</style>
