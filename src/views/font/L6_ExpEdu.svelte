<script>
  import { onMount } from 'svelte';

  let intercept = 27.2188;
  let coef_educ = 1.3843;
  let coef_race_black = -3.6740 ;
  let coef_educ_race_black = -0.2437;
  let coef_age = 0.1460;

  // Simplified script without the predictive logic and reactive statements

  function renderLatex() {
    const equation = `\\text{Predicted Wage   } Wage = 27.22 + 
    (1.38 \\times Education) + 
    (-3.67 \\times Black) + 
    {\\color{red}{(${coef_educ_race_black.toFixed(2)} \\times Education \\times Black)}} + 
    (0.15 \\times Age)`;
    const options = { throwOnError: false };
    katex.render(equation, document.getElementById('staticEquation'), options);
  }

  onMount(() => {
    renderLatex(); // Render your static LaTeX equation once on component mount
  });
</script>

<div class="fontBox">
  <h1 class="fontBox_1">Feel free to play with the bar to change the input number of education and how it makes a difference for hourly wage.</h1>
  <div class="fontBox_2">
    <h1 class="fontBox_2">To unravel this mystery, we turn to linear regression, to probe the factors influencing wages beyond mere education levels</h1>
  </div>
  <div id="staticEquation"></div>
  <div class="scroll-message-container">
    <div class="scroll-arrow">
      ↓
    </div>
    <p class="scroll-text">Scroll down at the left center to keep exploring</p>
  </div>
</div>
<style>
  .fontBox{
    padding: 0px;
  }
  .fontBox_1{
    font-weight: 600;
    font-size: 40px;
  }    
  .fontBox_2{
    font-weight: 400;
    font-size: 24px;
  }  
  .scroll-message-container {
    position: absolute; /* or absolute, depending on your layout */
    bottom: 20px; /* Adjust as needed */
    left: 15%; /* Center horizontally */
    transform: translateX(-50%);
    display: flex;
    align-items: center;
    justify-content: center;
    animation: bounce 2s infinite; /* Animation for the arrow */
    cursor: pointer; /* Optional, if you want to make it clickable */
  }

  .scroll-arrow {
    font-size: 30px; /* Adjust size as needed */
    margin-right: 10px; /* Space between arrow and text */
  }

  .scroll-text {
    font-size: 24px; /* Adjust size as needed */
    color: #000000; /* Adjust color as needed */
  }

  @keyframes bounce {
    0%, 20%, 50%, 80%, 100% {
      transform: translateY(0);
    }
    40% {
      transform: translateY(-20px);
    }
    60% {
      transform: translateY(-10px);
    }
  }
</style>