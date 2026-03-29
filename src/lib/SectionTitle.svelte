<script>
  let { title } = $props();
</script>

<div class="flex items-center gap-3">
  <h2
    class="text-[11px] font-semibold tracking-[0.2em] text-slate-600 uppercase md:text-sm dark:text-slate-300"
  >
    {title}
  </h2>
  <span
    class="h-px flex-1 bg-gradient-to-r from-slate-300 to-transparent dark:from-slate-700"
  ></span>
</div>
