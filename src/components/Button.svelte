<script>
  let clazz;
  export { clazz as class };

  // export let click;
</script>

<button on:click class={`group relative h-9 w-16 rounded-md bg-zinc-200 p-2 ring-zinc-400 transition-all hover:ring-2 dark:bg-zinc-700 ${clazz || ''}`} type="submit">
  <slot />
</button>
