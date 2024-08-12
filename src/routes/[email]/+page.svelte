<script lang="ts">
  import { page } from "$app/stores";
  import { getPokemonList, getPokemon } from "$lib/pokemonAPI";
  $: email = $page.params.email;

  let pokemonList: any = [];
  let pokemonData: any = [];
  let profile: any = {
    description: "Cool description",
    pokemon_ids: [1, 2, 3],
  };

  async function refreshPokemonData() {
    pokemonData = [];
    profile.pokemon_ids.map(async (id: number) => {
      const data = await getPokemon(id.toString());
      pokemonData = pokemonData ? [...pokemonData, data] : [data];
    });
  }
  page.subscribe(async () => {
    pokemonList = await getPokemonList();
    await refreshPokemonData();
    console.log(await getPokemon("pikachu"));
    console.log(pokemonList);
    console.log(pokemonData);
  });
</script>

<div class="hero min-h-screen bg-base-300">
  <div class="hero-content">
    <div class="max-w-2xl text-center">
      <h1 class="font-bold text-4xl">{email}'s Page</h1>
      <p class="py-3 max-w-md mx-auto">User description here...</p>
      <div class="grid grid-cols-3">
        {#if !pokemonData}
          <p>Loading...</p>
        {:else}
          {#each pokemonData as pokemon}
            <div class="card bg-slate-700 m-4 shadow-lg shadow-blue-900">
              <div class="card-body">
                <div class="text-center">
                  <img
                    src={pokemon.sprites.front_default}
                    alt="Pokemon Img"
                    class="w-32 h-32 mx-auto"
                  />
                  <h2 class="text-white text-2xl font-bold">{pokemon.name}</h2>
                  <p class="text-info">{pokemon.types[0].type.name}</p>
                </div>
              </div>
            </div>
          {/each}
        {/if}
      </div>
    </div>
  </div>
</div>
