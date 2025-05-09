<script lang="ts">
  import { cn } from "$lib/utils";
  let {
    value = $bindable(""),
    placeholder = "",
    class: className = "",
  }: { value?: string; placeholder?: string; class?: string } = $props();

  let showPlaceholder = $derived(!(value.length > 0));

  function oninput() {
    value = value.replace(/\n/g, "");
  }

  function onkeydown(event: KeyboardEvent) {
    if (event.key === "Enter") {
      event.preventDefault();
    }
  }
</script>

<div
  bind:innerText={value}
  contenteditable="plaintext-only"
  aria-roledescription="textbox"
  role="textbox"
  tabindex="0"
  {onkeydown}
  {oninput}
  {placeholder}
  spellcheck="false"
  class={cn(
    "ring-offset-background focus-visible:ring-ring focus-visible:outline-none focus-visible:ring-2 focus-visible:ring-offset-2",
    "px-3 py-2 h-min rounded-md",
    showPlaceholder &&
      "before:content-[attr(placeholder)] before:opacity-50 before:pointer-events-none",
    className
  )}

></div>
