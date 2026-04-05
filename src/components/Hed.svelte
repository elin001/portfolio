<script>
  import { cubicInOut } from "svelte/easing";
  import { fade } from "svelte/transition";
  let { isDesktop } = $props();
</script>

<div class="hed-wrapper">
  <h1 transition:fade={{ delay: 150, duration: 600, easing: cubicInOut }}>
    {#if !isDesktop}
      Ellie Lin
    {:else}
      Hi, I'm <span class="emphasis">Ellie Lin</span>,
      <br /> visual journalist
    {/if}
  </h1>
</div>

<style>
  .hed-wrapper {
    margin: 15rem 0 1rem;
  }
</style>