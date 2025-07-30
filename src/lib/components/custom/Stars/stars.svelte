<script lang="ts">
  // credit: https://uiverse.io/amikambs/dangerous-impala-17
  import { cn } from "$lib/utils";

  let { class: className = "", value = $bindable(0), size = 5, disabled = false } = $props();

  // Helper to determine star type
  function getStarType(index: number) {
    if (value >= index + 1) return "full";
    if (value >= index + 0.5) return "half";
    return "empty";
  }
</script>

<div
  class={cn(
    "flex flex-row items-center text-4xl gap-0.5 p-0 cursor-pointer",
    disabled && "pointer-events-none",
    "rounded-md  focus-within:[&:has(:focus-visible)]:ring-ring/50 focus-within:[&:has(:focus-visible)]:border-ring aria-invalid:ring-destructive/20 dark:aria-invalid:ring-destructive/40 aria-invalid:border-destructive outline-none transition-all focus-within:[&:has(:focus-visible)]:ring-[3px]",
    className
  )}
>
  <input
    class="appearance-none absolute peer"
    type="radio"
    tabindex="0"
    value={0}
    bind:group={value}
    {disabled}
  />
  {#each Array(size).fill(0) as _, index}
    <label class={cn("cursor-pointer", disabled && "cursor-auto")}>
      <input
        class="appearance-none absolute peer"
        type="radio"
        tabindex="0"
        value={index + 1 == value ? 0 : index + 1}
        bind:group={value}
        {disabled}
      />

      <svg
        viewBox="0 0 576 512"
        height="0.5em"
        xmlns="http://www.w3.org/2000/svg"
        class={getStarType(index) == "full" ? "fill-amber-500" : "fill-gray-400/50"}
      >
        <path
          d="M316.9 18C311.6 7 300.4 0 288.1 0s-23.4 7-28.8 18L195 150.3 51.4 171.5c-12 1.8-22 10.2-25.7 21.7s-.7 24.2 7.9 32.7L137.8 329 113.2 474.7c-2 12 3 24.2 12.9 31.3s23 8 33.8 2.3l128.3-68.5 128.3 68.5c10.8 5.7 23.9 4.9 33.8-2.3s14.9-19.3 12.9-31.3L438.5 329 542.7 225.9c8.6-8.5 11.7-21.2 7.9-32.7s-13.7-19.9-25.7-21.7L381.2 150.3 316.9 18z"
        ></path>
        {#if getStarType(index) === "half"}
          <path
            class="fill-amber-500"
            style="clip-path: inset(0 50% 0 0);"
            d="M316.9 18C311.6 7 300.4 0 288.1 0s-23.4 7-28.8 18L195 150.3 51.4 171.5c-12 1.8-22 10.2-25.7 21.7s-.7 24.2 7.9 32.7L137.8 329 113.2 474.7c-2 12 3 24.2 12.9 31.3s23 8 33.8 2.3l128.3-68.5 128.3 68.5c10.8 5.7 23.9 4.9 33.8-2.3s14.9-19.3 12.9-31.3L438.5 329 542.7 225.9c8.6-8.5 11.7-21.2 7.9-32.7s-13.7-19.9-25.7-21.7L381.2 150.3 316.9 18z"
          ></path>
        {/if}
      </svg>
    </label>
  {/each}
</div>
