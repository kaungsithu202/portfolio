<script lang="ts">
  import type { Snippet } from "svelte";

  let {
    href,
    children,
  }: {
    href: string;
    children?: Snippet;
  } = $props();
</script>

<a
  {href}
  target="_blank"
  rel="noopener noreferrer"
  class="inline-flex w-fit items-center justify-center rounded-lg border border-slate-200/90 bg-white/70 p-2 text-slate-700 shadow-[0_10px_20px_-16px_rgba(15,23,42,0.8)] transition hover:-translate-y-0.5 hover:border-cyan-300 hover:text-cyan-700 dark:border-slate-700 dark:bg-slate-900/60 dark:text-slate-200 dark:hover:border-cyan-700 dark:hover:text-cyan-300"
>
  {@render children?.()}
</a>
