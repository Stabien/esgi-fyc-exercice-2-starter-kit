<script>
  import { Router, Route } from 'svelte-navigator';
  import Home from './routes/Home.svelte';
  import Recipes from './routes/Recipes.svelte';
  import Recipe from './routes/RecipeDetails.svelte';
  import Navbar from './lib/Navbar.svelte';
</script>

<Router>
  <Navbar />
  <div>
    <Route path="/" component={Home} />
    <Route path="/recipes/search/:search" component={Recipes} />
    <Route path="/recipes/:id" let:params>
      <Recipe id={params.id} />
    </Route>
  </div>
</Router>

<style>
  @font-face {
    font-family: 'Roboto';
    font-style: normal;
    font-weight: 400;
    src: url('%sveltekit.assets%/Roboto-Regular') format('ttf');
  }

  :global(h1) {
    outline: none;
  }

  :global(body) {
    padding: 0;
    margin: 0;
    font-family: 'Roboto';
    background-color: #f9f9f9;
  }
</style>
