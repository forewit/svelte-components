<script lang="ts">
  import Button, { type ButtonProps } from "$lib/components/ui/button/button.svelte";
  import { onDestroy } from "svelte";

  let {
    onclick = () => {},
    duration = 2000,
    children,
    ...restProps
  }: { onclick?: () => void; duration?: number } & ButtonProps = $props();

  let progress = $state(0);
  let completed = $state(false);
  let timer: number | null = null;
  let startTime: number | null = null;

  function reset() {
    progress = 0;
    completed = false;
    startTime = null;
    if (timer) {
      cancelAnimationFrame(timer);
      timer = null;
    }
  }

  function startHold() {
    reset();
    startTime = performance.now();
    progress = 0;
    completed = false;
    animate();
  }

  function animate() {
    if (startTime === null) return;
    const now = performance.now();
    progress = Math.min((now - startTime) / duration, 1);
    if (progress < 1) {
      timer = requestAnimationFrame(animate);
    } else {
      progress = 1;
      completed = true;
      timer = null;
    }
  }

  $effect(()=>{
    if (completed) {
        onclick();
        reset();
    }
  })

  onDestroy(reset);
</script>

<svelte:window onpointerup={reset} />

<Button
  {...restProps}
  onpointerdown={startHold}
  onpointerleave={reset}
  onclick={(e)=>{
    e.preventDefault();
    e.stopPropagation();
  }}
  class="relative overflow-hidden select-none"
>
  <div
    aria-hidden="true"
    class="absolute top-0 left-0 bottom-0 bg-white/30 pointer-events-none z-1"
    style="width: {progress * 100}%;"
  ></div>

  {@render children?.()}
</Button>
