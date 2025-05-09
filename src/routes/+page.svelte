<script lang="ts">
  import { base } from "$app/paths";
  import Segment from "$lib/components/custom/7segment/7segment.svelte";
  import DollarInput from "$lib/components/custom/DollarInput/dollar-input.svelte";
  import Ecard from "$lib/components/custom/eCard/ecard.svelte";
  import Editor from "$lib/components/custom/editor/editor.svelte";
  import Heart from "$lib/components/custom/Heart/heart.svelte";
  import Stars from "$lib/components/custom/Stars/stars.svelte";
  import WrappedInput from "$lib/components/custom/WrappedInput/wrapped-input.svelte";
  import Button from "$lib/components/ui/button/button.svelte";
  import Label from "$lib/components/ui/label/label.svelte";
  import { Github } from "lucide-svelte";
  import { type Snippet } from "svelte";
</script>

<div class="grid items-center justify-center gap-2 p-4">
  <div class="flex items-center gap-2">
    <img src="{base}/favicon.png" alt="Logo" class="w-16 h-16 -mb-1 -ml-2" />
    <h1 class="text-3xl font-bold">Svelte Components</h1>
  </div>
  <div class="flex justify-center">
    <Button href="https://github.com/forewit/svelte-components" class="w-min">
      <Github /> View on GitHub
    </Button>
  </div>
</div>


<div class="flex flex-wrap justify-center gap-10 p-6">
  <div class="grid justify-items-center gap-4 p-4 bg-muted rounded-lg h-min">
    <Label>Stars</Label>
    <Stars size={4} value={3} />
  </div>
  <div class="grid justify-items-center gap-4 p-4 bg-muted rounded-lg h-min">
    <Label>Heart</Label>
    <Heart />
  </div>

  <div class="grid justify-items-center gap-4 p-4 bg-muted rounded-lg h-min">
    <Label>eCard</Label>
    <Ecard color="hsl(220, 70%, 40%)" foil rotate />
  </div>

  <div class="grid justify-items-center gap-4 p-4 bg-muted rounded-lg h-min">
    <Label>7segement</Label>
    <Segment class="w-32 h-10 p-2" value="hi there" />
  </div>

  <div class="grid justify-items-center gap-4 p-4 bg-muted rounded-lg h-min">
    <Label>Wrappable Input</Label>
    <div class="p-4 rounded border-2 border-dashed border-red-700 w-64">
      <p class="text-sm text-red-700 pb-4">Single line input that wraps:</p>
      <WrappedInput class="border" placeholder="Type here..." />
    </div>
  </div>

  <div class="grid justify-items-center gap-4 p-4 bg-muted rounded-lg h-min">
    <Label>Dollar Input</Label>
    <DollarInput class="border" />
  </div>

  <div class="grid justify-items-center gap-4 p-4 bg-muted rounded-lg h-min">
    <Label>Block Editor</Label>
    <Editor class="w-64" />
  </div>
</div>
