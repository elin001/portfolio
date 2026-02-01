<script>
  let { offTheClock, isMobile } = $props();
</script>

{#if isMobile}
  <h1>Ellie Lin</h1>
{:else}
  <h1>
    Hi, I’m <span class="emphasis">Ellie Lin,</span>
    <br />visual journalist
  </h1>
{/if}
 