<script>
  import { goto } from "$app/navigation";
  import "../app.pcss";
</script>

<div class="bg-base-100 justify-between fixed top-0 left-0 right-0">
  <div class="navbar max-w-3xl mx-auto justify-between">
    <div>
      <a href="/" class="btn btn-ghost text-xl">PokePage</a>
      <a href="/user" class="btn btn-ghost">My Page</a>
    </div>
    <div>
      <button on:click={() => goto("/login")}>Login</button>
      <span class="font-bold text-lg ml-2">randomUser@icloud.com</span>
      <button on:click={() => console.log("logging out")}>Logout</button>
    </div>
  </div>
</div>

<slot></slot>
