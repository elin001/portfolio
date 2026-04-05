<script>
  import FeaturedImage from "./FeaturedImage.svelte";
  let { isMobile, article } = $props();
</script>

<!-- to do: import format from D3 to format month date -->

<div class="entry">
  {#if article.img}
    {#each article.img as img, i}
      <FeaturedImage {img} />
    {/each}
  {:else}
    <FeaturedImage img={"rectangle.png"} />
  {/if}
  <h2>
    <a href={article.link} target="_blank">{article.headline}</a>
  </h2>
  <p class="publication">
    {article.publication}
    {#if isMobile}
        <br />
      <span class="date"> {article.date}</span>
    {:else}
      <span class="date"> | {article.date}</span>
    {/if}
  </p>
</div>

<style>
  .entry {
    display: flex;
    flex-flow: column wrap;
    row-gap: 4px;
    max-width: screen;
    margin: 1rem 0;
  }
</style>
