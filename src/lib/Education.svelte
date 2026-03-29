<script>
  let { name, level } = $props();
</script>

<div
  class="flex w-full flex-col gap-2 rounded-xl border border-slate-200/80 bg-white/70 p-3 backdrop-blur md:flex-row md:items-center md:justify-between md:p-4 dark:border-slate-700/70 dark:bg-slate-900/45"
>
  <p class="text-xs font-semibold tracking-[0.08em] md:text-sm">{name}</p>
  <p class="text-[10px] text-slate-600 uppercase md:text-xs dark:text-slate-300">
    {level}
  </p>
</div>
