<script>
  import data from "../data/portfolio.json";

  import Hed from "./components/Hed.svelte";

  let innerWidth = $state(0);
  let isMobile = $derived(innerWidth < 768);
  let isTablet = $derived(innerWidth >= 768 && innerWidth < 1024);
  let isDesktop = $derived(innerWidth >= 1024);

  let offTheClock = $state(false);

  $inspect(data);
</script>

<svelte:window bind:innerWidth />

<Hed {offTheClock} {isMobile} />

<style>
</style>
