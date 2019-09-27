<script>
   import { createEventDispatcher } from 'svelte';
   export let query;
   export let submitButtonText = "Search";

   const dispatch = createEventDispatcher();

   function handleSearch() {
      dispatch('search', {
         query
      })
   }
</script>

<style>
   .search-bar {
      height: 50px;
      width: 100%;
      padding: .5rem;
      background: #d1d1d1;
   }

   .search-bar input {
      font-size: 16px;
   }
</style>

<div class="search-bar">
   <form on:submit|preventDefault={handleSearch}>
      <input bind:value={query} />
      <button>{submitButtonText}</button>
   </form>
</div>