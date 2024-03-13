<script>
  import { onMount } from 'svelte';
  let displayedMessages = []; // Array to hold messages that are currently displayed
  const messages = [
    "What are the long-term impacts of educational return disparities on society?",
    "What are some of the potential factors that could lead to a wage gap?",
    "How can the education system be improved to ensure a fairer return on investment for all?"
  ];
  let line = 0; // Current line being displayed

  function displayNextSentence() {
    if (line < messages.length) {
      // Add the current line to displayedMessages
      displayedMessages = [...displayedMessages, messages[line]];
      line++;
    }
  }

  onMount(() => {
    const interval = setInterval(() => {
      displayNextSentence();
      if (line === messages.length) {
        clearInterval(interval); // Stop when all lines have been displayed
      }
    }, 500); // Display next sentence every 500 milliseconds
  });
</script>
<div class="introduction">
  <h1 style="font-weight: 700; font-size: 40px;">Through this project we want you to think about:</h1>
  {#each displayedMessages as message, i}
    <!-- Apply special style for the specific message, general style for others -->
    {#if message === "Through this project we want you to think about:"}
      <div style="font-weight: 500; font-size: 30px;">{message}</div>
    {:else}
      <!-- Apply a general font size to all other messages -->
      <div style="font-size: 20px;">{i > 0 ? '• ' : ''}{message}</div>
    {/if}
  {/each}
</div>

<style>
  .introduction {
    width: 100%;
    padding: 20px;
    background-color: #f3f3f3;
    border-radius: 8px;
    font-family: Arial, sans-serif;
    color: #333;
    line-height: 2;
    text-align: center;
    height: 100%;
  }
</style>
  