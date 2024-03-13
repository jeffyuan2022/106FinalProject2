<script>
    import { onMount } from 'svelte';
    let displayedMessages = []; // Array to hold messages that are currently displayed
    const messages = [
      "It's commonly understood that higher education often translates into higher wages.",
      "However, one might wonder:",
      "if the wage gap could simply be explained by differences in education levels. After all, it's a common assumption that higher education leads to higher wages. But does this theory hold up when we examine the data?"
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
    {#each displayedMessages as message, i}
      <!-- Check for specific messages to apply unique styles -->
      {#if message === "However, one might wonder:" || message === "It's commonly understood that higher education often translates into higher wages."}
        <div style="font-weight: 500; font-size: 30px;">{message}</div>
      {:else}
        <!-- Apply a general font size to all other messages -->
        <br>
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