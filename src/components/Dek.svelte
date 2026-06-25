<script>
  import { fly } from 'svelte/transition';
  import { cubicOut, cubicIn } from 'svelte/easing';

  let { isMobile } = $props();

  const activities = [
    { phrase: "love to ride my bike ", url: "https://cycle-1k.vercel.app"},
    { phrase: "play ultimate frisbee", url: "" },
    { phrase: "cook really involved and time-consuming meals", url: "" },
    { phrase: "read books about plagues", url: "" },
  ];

  let currentIndex = $state(Math.floor(Math.random() * activities.length));

  $effect(() => {
    const interval = setInterval(() => {
      currentIndex = (currentIndex + 1) % activities.length;
    }, 10000);
    return () => clearInterval(interval);
  });

  let scrollY = $state(0);
  let p1visible = $derived(scrollY > 10);
  let p2visible = $derived(scrollY > 150);
</script>

<svelte:window bind:scrollY />

<p
  class={[
    "text-ink font-sans text-2xl font-normal tracking-[-0.01em] leading-normal mb-4 max-md:text-[1.25rem] max-md:leading-[1.25] max-md:my-4",
    "para-fade",
    p1visible && "para-visible",
  ]}
>
  {#if isMobile}
    Hi! I'm a visual journalist, specializing in news and information design.
  {:else}
    I like breaking down complex concepts into impactful stories, working
    creatively across mediums and getting important information to people who
    need it.
  {/if}
</p>

<p
  class={[
    "text-ink font-sans text-2xl font-normal tracking-[-0.01em] leading-normal pt-5 mb-4 max-md:text-[1.25rem] max-md:leading-[1.25] max-md:my-4",
    "para-fade",
    p2visible && "para-visible",
  ]}
>
  {#if isMobile}
    I like breaking down complex concepts into impactful stories, working
    creatively across mediums and getting important information to people who
    need it.
  {:else}
    I'm a news designer at The Minnesota Star Tribune during the day. Off the clock, I
    <span class="inline-grid overflow-hidden">
      {#key currentIndex}
        {#if activities[currentIndex].url}
          <a
            href={activities[currentIndex].url}
            style="grid-area: 1/1"
            class="text-inherit no-underline hover:text-accent transition-colors"
            in:fly={{ y: 20, duration: 350, easing: cubicOut }}
            out:fly={{ y: -20, duration: 350, easing: cubicIn }}
          >{activities[currentIndex].phrase}</a>
        {:else}
          <span
            style="grid-area: 1/1"
            in:fly={{ y: 20, duration: 350, easing: cubicOut }}
            out:fly={{ y: -20, duration: 350, easing: cubicIn }}
          >{activities[currentIndex].phrase}</span>
        {/if}
      {/key}
    </span>.
  {/if}
</p>

<style>
  .para-fade {
    opacity: 0;
    transform: translateY(12px);
    transition: opacity 0.6s ease, transform 0.6s ease;
  }

  .para-visible {
    opacity: 1;
    transform: translateY(0);
  }
</style>
