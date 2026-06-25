<script>
  import { cubicInOut } from "svelte/easing";
  import { fade } from "svelte/transition";
  let { isDesktop } = $props();
</script>

<div class="mx-auto mb-4 my-10">
  <h1
    transition:fade={{ delay: 150, duration: 600, easing: cubicInOut }}
    class="text-ink font-dm-bold text-[4.5rem] md:text-[5rem] leading-25 text-left md:text-center"
  >
    {#if !isDesktop}
      <span class="aurora">Ellie Lin</span>
    {:else}
      Hi, I'm <span
        class="text-accent font-dm-bold text-[5rem] font-bold leading-20 tracking-[-2.88px]"
      >Ellie Lin,</span>
      <br /> news designer
    {/if}
  </h1>
</div>

<style>
  .aurora {
    background: linear-gradient(
      120deg,
      #000313 0%,
      #000313 30%,
      #819bff 50%,
      #000313 70%,
      #000313 100%
    );
    background-size: 300% 100%;
    background-clip: text;
    -webkit-background-clip: text;
    color: transparent;
    animation: aurora-sweep 20s ease-in-out infinite;
  }

  @keyframes aurora-sweep {
    0%   { background-position: 100% 0%; }
    50%  { background-position: 0% 0%; }
    100% { background-position: 100% 0%; }
  }
</style>
