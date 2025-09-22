<script>
  let { name, level } = $props();
</script>

<div class="flex items-start justify-between w-full mt-3">
  <p class="font-bold text-xs md:text-base">{name}</p>
  <p class="font-medium text-[10px] md:text-sm">{level}</p>
</div>
