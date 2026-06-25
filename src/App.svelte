<script>
  import { groups } from "d3-array";
  import data from "../data/portfolio.json";

  import Hed from "./components/Hed.svelte";
  import Entry from "./components/Entry.svelte";
  import Dek from "./components/Dek.svelte";

  let innerWidth = $state(0);
  let isMobile = $derived(innerWidth < 768);
  let isDesktop = $derived(innerWidth >= 1024);

  let activeTag = $state(null);

  // Sort entries oldest → newest within each group, then group by tag.
  // Group order is determined by the most recent entry in each group.
  const parseDate = (d) => new Date(d.date);
  const sortedData = [...data].sort((a, b) => parseDate(b) - parseDate(a));

  let groupedData = $derived(
    groups(sortedData, (d) => d.tags).sort((a, b) => {
      const aLatest = Math.max(...a[1].map((d) => parseDate(d)));
      const bLatest = Math.max(...b[1].map((d) => parseDate(d)));
      return bLatest - aLatest;
    }),
  );

  let sectionEls = $state([]);

  $effect(() => {
    const els = sectionEls.filter(Boolean);
    if (!els.length) return;

    const observer = new IntersectionObserver(
      (entries) => {
        const visible = entries
          .filter((e) => e.isIntersecting)
          .sort((a, b) => b.intersectionRatio - a.intersectionRatio)[0];
        if (!visible) return;
        activeTag = visible.target.dataset.tag;
      },
      {
        root: null,
        threshold: Array.from({ length: 11 }, (_, i) => i / 10),
        rootMargin: "-30% 0px -30% 0px",
      },
    );

    els.forEach((el) => observer.observe(el));
    return () => observer.disconnect();
  });
</script>

<svelte:window bind:innerWidth />

<div class="flex flex-col mx-auto">
  <section class="mx-auto my-[25dvh] md:max-w-[800px]">
    <Hed {isDesktop} />
    <Dek {isMobile} />
  </section>

  <section class="max-w-[55rem] mx-auto mt-2.5 flex flex-col gap-12 pb-16">
    {#each groupedData as [tag, articles], i}
      <div
        class="grid grid-cols-[8rem_1fr] gap-8 items-start max-md:flex max-md:flex-col"
        data-tag={tag}
        bind:this={sectionEls[i]}
      >
        <div
          class={[
            "sticky top-[40vh] font-sans-extralight text-3xl tracking-[0.08em] leading-snug transition-colors duration-300 pt-4 text-right",
            "max-md:top-0 max-md:text-center max-md:bg-[rgba(255,253,255,0.92)] max-md:w-full max-md:px-3 max-md:py-1.5 max-md:mx-auto max-md:mb-2 max-md:z-10",
            activeTag === tag ? "text-accent" : "text-ink",
          ]}
        >
          {tag}
        </div>
        <div class="flex flex-col">
          {#each articles as article}
            {#if article.featured}
              <Entry {isMobile} {article} />
            {/if}
          {/each}
        </div>
      </div>
    {/each}
  </section>
</div>
