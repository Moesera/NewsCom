<!-- Possible vulnerability: If user generated, user can generate malicious link -->

<script lang="ts">
  import { Link } from "svelte-routing";

  export let buttonText = "Click me";
  export let disabled = false;
  export let type: "button" | "submit" | "reset" = "button";
  export let classList = "";
  export let to = "";
</script>

<!-- The button component can be used to create a button or a hyperlink. -->

{#if to}
  <Link {to} class={classList}>
    {buttonText}
  </Link>
{:else}
  <button class={classList} {type} {disabled}>
    {buttonText}
  </button>
{/if}

<style>
  button {
    border-radius: 3px;
    border: 1px solid transparent;
    padding: 0.6em 1.2em;
    font-size: 1em;
    font-weight: 500;
    font-family: inherit;
    cursor: pointer;
    transition: border-color 0.25s;
    background-color: #e5e5e5;
  }

  button:hover {
    border-color: #646cff;
  }

  button:focus,
  button:focus-visible {
    outline: 4px auto -webkit-focus-ring-color;
  }
</style>
