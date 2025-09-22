<script>
  import { Globe } from "@lucide/svelte";

  let { image, name, description, techStacks, link } = $props();
</script>

<div class="border p-1.5 rounded-md border-gray-200 z-50 bg-white/50">
  <img src={image} alt={name} class="rounded-md" />

  <h2 class="mt-3 text-sm md:text-base">{name}</h2>

  <p class="text-[10px] md:text-xs text-slate-700 mt-1.5">
    {description}
  </p>

  <div class="flex items-center gap-1 flex-wrap mt-1.5">
    {#each techStacks as tech (tech)}
      <div
        class="bg-gray-600 text-sm md:text-base text-white w-fit text-[10px] rounded-md py-1 px-2"
      >
        {tech}
      </div>
    {/each}
  </div>

  <a
    href={link}
    target="_blank"
    class="bg-white border w-fit rounded-lg p-1 text-[10px] flex items-center gap-2 mt-1.5"
  >
    <Globe size="12" /> Website
  </a>
</div>
