<script>
  import { fly, fade } from 'svelte/transition';
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
    }, 5000);
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
    <span class="inline-grid" style="min-width: max-content; overflow: visible">
      {#key currentIndex}
        <span
          style="grid-area: 1/1"
          in:fly={{ y: 16, duration: 400, easing: cubicOut }}
          out:fly={{ y: -16, duration: 300, easing: cubicIn }}
        >
          {#if activities[currentIndex].url}
            <a
              href={activities[currentIndex].url}
              class="text-inherit no-underline hover:text-accent transition-colors"
            >{activities[currentIndex].phrase}</a>
          {:else}
            {activities[currentIndex].phrase}
          {/if}
        </span>
      {/key}
    </span>.
  {/if}
</p>

<div
  class={[
    "flex items-center gap-3 pt-4 para-fade",
    p2visible && "para-visible",
  ]}
>
  <span class="font-sans text-xl text-ink tracking-[-0.01em]">Get in touch:</span>
  <a href="mailto:ellie.ellielin@gmail.com" aria-label="Email" class="text-ink hover:text-accent transition-colors">
    <!-- Mail icon: https://heroicons.com/ (MIT) -->
    <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" width="28" height="28" aria-hidden="true">
      <path stroke-linecap="round" stroke-linejoin="round" d="M21.75 6.75v10.5a2.25 2.25 0 0 1-2.25 2.25h-15a2.25 2.25 0 0 1-2.25-2.25V6.75m19.5 0A2.25 2.25 0 0 0 19.5 4.5h-15a2.25 2.25 0 0 0-2.25 2.25m19.5 0v.243a2.25 2.25 0 0 1-1.07 1.916l-7.5 4.615a2.25 2.25 0 0 1-2.36 0L3.32 8.91a2.25 2.25 0 0 1-1.07-1.916V6.75" />
    </svg>
  </a>
  <a href="https://www.linkedin.com/in/ellie-d-lin" aria-label="LinkedIn" target="_blank" rel="noopener noreferrer" class="text-ink hover:text-accent transition-colors">
    <!-- LinkedIn icon: https://simpleicons.org/ (CC0) -->
    <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="currentColor" width="26" height="26" aria-hidden="true">
      <path d="M20.447 20.452h-3.554v-5.569c0-1.328-.027-3.037-1.852-3.037-1.853 0-2.136 1.445-2.136 2.939v5.667H9.351V9h3.414v1.561h.046c.477-.9 1.637-1.85 3.37-1.85 3.601 0 4.267 2.37 4.267 5.455v6.286zM5.337 7.433a2.062 2.062 0 0 1-2.063-2.065 2.064 2.064 0 1 1 2.063 2.065zm1.782 13.019H3.555V9h3.564v11.452zM22.225 0H1.771C.792 0 0 .774 0 1.729v20.542C0 23.227.792 24 1.771 24h20.451C23.2 24 24 23.227 24 22.271V1.729C24 .774 23.2 0 22.222 0h.003z"/>
    </svg>
  </a>
</div>

<style>
  .para-fade {
    opacity: 0;
    transform: translateY(12px);
    transition: opacity 0.5s ease, transform 2s ease;
  }

  .para-visible {
    opacity: 1;
    transform: translateY(0);
  }
</style>
