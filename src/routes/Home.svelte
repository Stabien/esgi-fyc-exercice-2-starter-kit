<script>
  import { fade } from 'svelte/transition';
  import RecipeList from '../lib/RecipeList.svelte';
  import { fetchRecipes } from '../services';
</script>

<div class="container">
  <h1>Bienvenue sur Sveltmiton</h1>
  <h2>Nos recettes du jour</h2>
  {#await fetchRecipes()}
    <span>Chargement des recettes du jour...</span>
  {:then recipes}
    <div in:fade={{ duration: 200 }}>
      <RecipeList recipes={recipes.filter((recipe) => recipe.isDaily)} />
    </div>
  {:catch}
    <span>Impossible de charger les recettes du jour</span>
  {/await}
</div>

<style>
  h1 {
    text-align: center;
    border-radius: 10px;
    color: #ff6f61;
    font-size: 24px;
    width: fit-content;
    padding: 10px 40px;
    margin: auto;
    margin-top: 40px;
    border: 2px solid #ff6f61;
  }
  .container {
    display: flex;
    flex-direction: column;
    width: fit-content;
    margin: auto;
  }

  div > :global(a) {
    text-decoration: none;
    color: #ff5f15;
    border: 2px solid #ff5f15;
    border-radius: 20px;
    padding: 8px;
    margin: auto;
    transition: 0.25s;
  }

  div > :global(a):hover {
    background-color: #ff5f15;
    color: white;
  }
</style>
