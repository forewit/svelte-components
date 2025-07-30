<script lang="ts">
  import Input from "$lib/components/ui/input/input.svelte";
  import { cn } from "$lib/utils";
  import type { HTMLInputAttributes } from "svelte/elements";

  type Props = Omit<
    HTMLInputAttributes,
    "value" | "disabled" | "type" | "inputmode" | "placeholder" | "files" | "min"
  > & {
    value: number;
    placeholder?: string;
    disabled?: boolean;
  };

  let {
    value = $bindable(0),
    disabled = false,
    class: className,
    placeholder = "0",
    ...restProps
  }: Props = $props();
</script>

{#if disabled}
  ${value.toFixed(2)}
{:else}
  <span
    class={cn("relative before:text-sm before:content-['$'] before:absolute before:top-1/2 before:-translate-y-1/2 before:left-3", className)}
  >
    <Input
      bind:value
      type="number"
      inputmode="decimal"
      {placeholder}
      class={cn(
        "text-right pl-6",
        className
      )}
      {...restProps}
    />
  </span>
{/if}
