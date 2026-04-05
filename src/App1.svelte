<script>
  import { groups } from "d3-array";
  import data from "./data/portfolio.json";

  import Hed from "./components/Hed.svelte";
  import Entry from "./components/Entry.svelte";
  import Dek from "./components/Dek.svelte";

  let innerWidth = $state(0);
  let isMobile = $derived(innerWidth < 768);
  let isTablet = $derived(innerWidth >= 768 && innerWidth < 1024);
  let isDesktop = $derived(innerWidth >= 1024);

  let offTheClock = $state(false);
  let activeSlug = $state(null);
  let sections = $state(null);

  let groupedData = $derived(
    groups(data, (d) => d.tags).sort(function (a, b) {
      return a - b;
    })
  );

  $effect(() => {
    if (!sections.length) return;
    const byId = new Map(data.map((d) => [d.tags, d]));

    const observer = new IntersectionObserver(
      (entries) => {
        const visible = entries
          .filter((e) => e.isIntersecting)
          .sort((a, b) => b.intersectionRatio - a.intersectionRatio)[0];

        if (!visible) return;

        const id = visible.target.id;
        if (!id) return;
        activeSlug = id;
      },
      {
        root: null,
        threshold: [0.1],
        rootMargin: "-20% 0px -10% 0px",
      }
    );
    sections.forEach((el) => observer.observe(el));

    return () => observer.disconnect();
  });
</script>

<svelte:window bind:innerWidth />

<div class="content">
  <section class="hedder">
    <Hed {isDesktop} />
    <Dek {isMobile} {offTheClock} />
  </section>
  <section class="body">
    <div bind:this={sections} id={activeSlug}>
      <div class="layout">
        {#each data as article, i}
          {#if article.featured}
            <Entry {isMobile} {article} />
          {/if}
        {/each}
      </div>
    </div>
  </section>
</div>
