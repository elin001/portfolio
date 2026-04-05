<script>
  let { isMobile, offTheClock = $bindable(false) } = $props();

  function clickTime() {
    offTheClock = !offTheClock;
  }
</script>

<p class="subhed">
  {#if isMobile}
    Hi! I’m a visual journalist, specializing in news and information design.
  {:else}
    I like breaking down complex concepts into impactful stories, working
    creatively across mediums and getting important information to people who
    need it.
  {/if}
</p>

<p class="subhed">
  {#if isMobile}
    I like breaking down complex concepts into impactful stories, working
    creatively across mediums and getting important information to people who
    need it.
  {:else}
    Currently, I’m a news designer at The Minnesota Star Tribune. <button
      class="clock"
      onclick={clickTime}>Off the clock</button
    >, I play ultimate frisbee, cook, and read books about plagues.
  {/if}
</p>

<style>
  .clock {
    color: #819bff;
    font-family: "General Sans Bold";
    font-weight: 700;
    font-size: inherit;
    cursor: pointer;
  }
</style>
