<script>
  import { Globe } from "@lucide/svelte";

  let { image, name, description, techStacks, link } = $props();
</script>

<article
  class="group z-50 rounded-2xl border border-slate-200/80 bg-white/75 p-2 backdrop-blur transition hover:-translate-y-1 hover:border-cyan-300/80 hover:shadow-[0_24px_60px_-44px_rgba(6,182,212,1)] md:p-3 dark:border-slate-700/70 dark:bg-slate-900/50 dark:hover:border-cyan-700/70"
>
  <div class="overflow-hidden rounded-xl border border-slate-200/70 dark:border-slate-700/70">
    <img
      src={image}
      alt={name}
      class="h-48 w-full object-cover transition duration-500 group-hover:scale-105"
    />
  </div>

  <div class="mt-3 px-1 pb-1">
    <div class="flex items-center justify-between gap-2">
      <h2 class="text-sm font-semibold md:text-base">{name}</h2>
      <a
        href={link}
        target="_blank"
        rel="noopener noreferrer"
        class="inline-flex items-center gap-1 rounded-md border border-slate-200 bg-white/80 px-2 py-1 text-[10px] transition hover:border-cyan-300 hover:text-cyan-700 md:text-xs dark:border-slate-700 dark:bg-slate-950/50 dark:hover:border-cyan-700 dark:hover:text-cyan-300"
      >
        <Globe size="12" /> Live
      </a>
    </div>

    <p class="mt-2 text-[10px] leading-5 text-slate-700 md:text-xs dark:text-slate-300">
      {description}
    </p>

    <div class="mt-3 flex flex-wrap items-center gap-1.5">
      {#each techStacks as tech (tech)}
        <div
          class="w-fit rounded-full border border-slate-300 bg-white/90 px-2 py-1 text-[9px] tracking-[0.08em] uppercase text-slate-700 md:text-[10px] dark:border-slate-700 dark:bg-slate-950/50 dark:text-slate-200"
        >
          {tech}
        </div>
      {/each}
    </div>
  </div>

</article>
