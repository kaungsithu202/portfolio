<script>
  import { ExternalLinkIcon } from "@lucide/svelte";

  let { company, position, timeline, link, image } = $props();
</script>

<div class="flex items-start justify-between w-full mt-5">
  <div class="flex items-center gap-3">
    <img
      src={image}
      class="rounded-full size-8 md:size-16"
      alt="Myanmar High Society"
    />
    <div>
      <p class="font-bold text-[10px] md:text-base">{company}</p>
      <p class="font-medium text-[10px] md:text-sm">{position}</p>
    </div>
  </div>

  <div class="flex items-center gap-1 md:gap-3">
    <p class="font-medium text-[8px] md:text-sm">{timeline}</p>
    <a
      href={link}
      class="border border-gray-200 dark:border-slate-700 p-[3px] rounded-md hover:bg-gray-100 dark:hover:bg-slate-800 transition-colors"
      target="_blank"
    >
      <ExternalLinkIcon class="md:size-4 size-2" />
    </a>
  </div>
</div>
