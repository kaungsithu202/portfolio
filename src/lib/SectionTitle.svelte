<script>
  let { title } = $props();
</script>

<div class="w-fit">
  <h2
    class="relative text-sm md:text-lg font-medium mt-5 after:content-[''] after:absolute after:left-0 after:bottom-0 after:w-0 after:h-[2px] after:bg-gray-600 dark:after:bg-slate-400 after:transition-all after:duration-300 hover:after:w-full mb-1.5"
  >
    {title}
  </h2>
</div>
