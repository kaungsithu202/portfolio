<script lang="ts">
  let { href } = $props();
</script>

<a
  {href}
  target="_blank"
  rel="noopener noreferrer"
  class="border border-gray-200 dark:border-slate-700 rounded-md w-fit p-1.5 hover:bg-gray-100 dark:hover:bg-slate-800 cursor-pointer transition-colors"
>
  <slot></slot>
</a>
