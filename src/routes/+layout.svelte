<script lang="ts">
  import "../app.css";
  import { ScrollArea } from "$lib/components/ui/scroll-area/index.js";
  import { ModeWatcher } from "mode-watcher";

  let { children } = $props();
</script>

<svelte:head>
  <title>Svelte Components</title>
</svelte:head>

<ModeWatcher />

<div
  class="h-screen w-screen grid relative pl-[env(safe-area-inset-left)] pr-[env(safe-area-inset-right)]"
>
  <ScrollArea type="scroll">
    <div class="max-w-[1200px] m-auto pt-[env(safe-area-inset-top)]">
      {@render children?.()}
    </div>
    <div class="pb-[env(safe-area-inset-bottom)]"></div>
  </ScrollArea>
</div>
