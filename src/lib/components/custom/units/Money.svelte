<script lang="ts">
  import Input from "$lib/components/ui/input/input.svelte";
  import type { HTMLInputAttributes } from "svelte/elements";

  type Props = Omit<
    HTMLInputAttributes,
    "value" | "disabled" | "type" | "inputmode" | "placeholder" | "files" | "min"
  > & {
    value: number;
    disabled?: boolean;
  };

  let { value = $bindable(0), disabled = false, ...restProps }: Props = $props();
</script>

{#if disabled}
  ${value.toFixed(2)}
{:else}
  <span
    class="relative before:content-['$'] before:absolute before:top-1/2 before:-translate-y-1/2 before:left-3"
  >
    <Input
      bind:value
      type="number"
      inputmode="decimal"
      placeholder="0"
      {...restProps}
      class="text-right pl-6"
    />
  </span>
{/if}
