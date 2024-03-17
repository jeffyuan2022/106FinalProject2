<script>
    import { onMount } from 'svelte';
    let text = ''; 
    // Break the message into an array of strings, each representing a bullet point
    const messages = [
      "This observation gently nudges us towards a deeper contemplation",
      "of the complexities behind these findings. It suggests that beyond",
      "the quantitative measures, there might be underlying systemic",
      "factors and societal dynamics influencing these outcomes. By",
      "clicking the choice after each designed question and self-exploring,",
      "adjusting the input values of each potential factor, we can more ",
      "clearly understand that there is always a gap in education return ",
      "between black and white people that contributes to wage disparities. ",
      "This reality beckons us to explore with kindness and curiosity: what ",
      "more can we understand and do to bridge this gap? Awareness and ",
      "intervention in addressing the root causes of inequality pave the ",
      "way for a more inclusive future. Let's continue this conversation ",
      "with openness, aiming to uncover and address the roots of this ",
      "disparity for a more equitable future."
    ];
    let index = 0;
    let line = 0; // New variable to keep track of the current line
  
    function typeWriter() {
      if (line < messages.length) {
        if (index < messages[line].length) {
          text += messages[line].charAt(index);
          index++;
        } else {
          text += "\n"; // Adds a newline at the end of each line/bullet point
          line++;
          index = 0;
        }
      }
    }
  
    onMount(() => {
      const interval = setInterval(typeWriter, 1);
      return () => clearInterval(interval);
    });
  </script>
  <div class="introduction">
    <!-- Update this part to iterate over the messages array and display each item as a bullet point -->
    {#each messages as message, i}
      {#if i < line}
        <div style="font-size: 18px"> {message}</div>
      {/if}
    {/each}
    
  </div>
  
  <style>
    .introduction {
      width: 100%;
      padding: 0px;
      background-color: #f3f3f3;
      border-radius: 10px;
      font-family: Arial, sans-serif;
      color: #333;
      line-height: 2;
      text-align: center; /* Align text to the left to match bullet points style */
      height: 100%;
    }
    img {
    width: 300px; /* Example width */
    height: auto; /* Maintain aspect ratio */
  }
  </style>