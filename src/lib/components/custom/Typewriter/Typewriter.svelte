<!-- a component for displaying text in a typed animation -->

<script lang="ts">
  import { onMount } from "svelte";

  let { minDelay = 30, maxDelay = 200, blinkDelay = 500, disableCursor = false } = $props();

  // state management
  let isBlinking = $state(true);
  let cursor = $state(" ");
  let displayedText: string = $state("");

  let timeoutID: ReturnType<typeof setTimeout>;

  // export function for starting the typewriter
  export const type = async (text:string) => {
    // reset then start typing
    reset();
    isBlinking = false;

    // loop through each char to type
    let delay: number;
    for (let i = 0; i < text.length; i++) {
      // delay for a bit between characters
      delay = randBetween(minDelay, maxDelay);

      // extend delay for a stylized effect
      if (text[i] == " ") delay *= 3;
      if (i > 0 && text[i-1].match(/[.,!]/)) delay += 500; 
      if (i > 0 && text[i-1] == "\n" && text[i] != "\n") delay += 800;
      
      // await delay then add the char
      await new Promise((res) => (timeoutID = setTimeout(res, delay)));
      displayedText += text[i];
    }

    // finished typing
    isBlinking = true;
    return Promise.resolve();
  };

  // export function to reset the typewriter
  export const reset = () => {
    clearTimeout(timeoutID);
    displayedText = "";
    isBlinking = true;
  };

  // helper function
  function randBetween(min: number, max: number) {
    return Math.floor(Math.random() * (max - min + 1)) + min;
  }

  // keep the cursor blinking
  function updateCursor() {
    if (disableCursor) cursor = " ";
    else if (!isBlinking) cursor = "|";
    else cursor = cursor == " " ? "|" : " ";
  }

  onMount(() => {
    setInterval(updateCursor, blinkDelay);
  });
</script>

<p style="white-space: pre-wrap;">{displayedText}{cursor}</p>
