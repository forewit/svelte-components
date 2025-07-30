<script lang="ts">
  import Input from "$lib/components/ui/input/input.svelte";
  import type { HTMLInputAttributes } from "svelte/elements";

  type Props = Omit<
    HTMLInputAttributes,
    "value" | "disabled" | "type" | "inputmode" | "placeholder" | "files" | "min"
  > & {
    value: number;
    symbol: string;
    disabled?: boolean;
  };

  let {
    value = $bindable(0),
    symbol = "#",
    disabled = false,
    ...restProps
  }: Props = $props();
</script>

{#if disabled}
  {value} {symbol}
{:else}
  <Input bind:value type="number" inputmode="decimal" placeholder="0" {...restProps} />
{/if}
