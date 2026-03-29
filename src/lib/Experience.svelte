<script>
  import { ExternalLinkIcon } from "@lucide/svelte";

  let { company, position, timeline, link, image } = $props();
</script>

<div
  class="rounded-xl border border-slate-200/80 bg-white/70 p-3 backdrop-blur md:p-4 dark:border-slate-700/70 dark:bg-slate-900/45"
>
  <div class="flex flex-col gap-3 md:flex-row md:items-center md:justify-between">
    <div class="flex items-center gap-3">
      <img
        src={image}
        class="size-10 rounded-xl object-cover ring-1 ring-slate-200 md:size-14 dark:ring-slate-700"
        alt={company}
      />
      <div>
        <p class="text-xs font-semibold tracking-[0.12em] md:text-sm">{company}</p>
        <p class="mt-1 text-[10px] text-slate-600 md:text-xs dark:text-slate-300">
          {position}
        </p>
      </div>
    </div>

    <div class="flex items-center gap-2 md:gap-3">
      <p
        class="text-[9px] tracking-[0.16em] text-slate-500 uppercase md:text-[11px] dark:text-slate-400"
      >
        {timeline}
      </p>
      <a
        href={link}
        class="inline-flex items-center gap-1 rounded-md border border-slate-200 bg-white/80 px-2 py-1 text-[10px] transition hover:border-cyan-300 hover:text-cyan-700 md:text-xs dark:border-slate-700 dark:bg-slate-950/50 dark:hover:border-cyan-700 dark:hover:text-cyan-300"
        target="_blank"
        rel="noopener noreferrer"
      >
        Company <ExternalLinkIcon class="size-3" />
      </a>
    </div>
  </div>
</div>
