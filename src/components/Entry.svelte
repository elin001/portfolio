<script>
  import FeaturedImage from "./FeaturedImage.svelte";
  let { isMobile, article } = $props();
</script>

<!-- to do: import format from D3 to format month date -->

<div class="flex flex-col flex-wrap gap-y-1 my-15 w-full">
  {#if article.img}
    <FeaturedImage img={article.img} />
  {/if}
  <h2
    class="text-ink font-sans-semibold text-[3.125rem] font-semibold leading-[1.2] text-left m-0 mb-4 text-balance max-md:text-[2rem] max-md:tracking-[-0.36px] max-md:mb-[0.2rem]"
  >
    <a href={article.link} target="_blank">{article.headline}</a>
  </h2>
  <p
    class="text-ink font-sans-medium text-2xl font-medium tracking-[-0.01em] leading-[1.3] text-left max-md:text-[1.25rem]"
  >
    {article.publication}
    {#if isMobile}
      <br />
      <span
        class="font-sans-extralight text-2xl font-extralight tracking-[-0.01em] max-md:text-[1.25rem]"
        >{article.date}</span
      >
    {:else}
      <span
        class="font-sans-extralight text-2xl font-extralight tracking-[-0.01em]"
      >
        | {article.date}</span
      >
    {/if}
  </p>
  {#if article.dek}
    <p class="font-sans text-[1.15rem] leading-6 text-pretty">{article.dek}</p>
  {/if}
</div>
