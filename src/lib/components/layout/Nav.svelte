<script lang="ts">
  import Button from "../page/Button.svelte";

  let links = [
    ["University search", "/"],
    ["Cat images", "/cats"],
    ["Stock prices", "/stocks"],
  ];
</script>

<nav>
  <ul>
    {#each links as [text, link]}
      <Button to={link} classList="nav-link" buttonText={text}></Button>
    {/each}
  </ul>
</nav>

<style>
  ul {
    display: flex;
    justify-content: center;
    gap: 0.5em;
  }
</style>
