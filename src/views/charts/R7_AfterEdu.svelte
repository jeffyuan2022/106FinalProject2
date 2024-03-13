<script>
    import { onMount } from 'svelte';
    let displayedMessages = []; // Array to hold messages that are currently displayed
    const messages = [
      "The results of our analysis shed light on a critical, yet often overlooked, aspect of the wage gap: ",
      " It appears that, on average, an additional year of education boosts the wages of White workers more significantly than it does for their Black counterparts."
  
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
      <!-- Apply special style for the specific message, general style for others -->
      {#if message === "The results of our analysis shed light on a critical, yet often overlooked, aspect of the wage gap: "}
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
      line-height: 3;
      text-align: center;
      height: 100%;
    }
  </style>