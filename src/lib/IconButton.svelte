<script lang="ts">
  let { href } = $props();
</script>

<a
  {href}
  target="_blank"
  rel="noopener noreferrer"
  class="border border-gray-200 rounded-md w-fit p-1.5 hover:bg-gray-100 cursor-pointer"
>
  <slot></slot>
</a>
