<script>
  import { onMount } from 'svelte';

  let intercept = 27.2188;
  let coef_educ = 1.3843;
  let coef_race_black = -3.6740 ;
  let coef_educ_race_black = -0.2437;
  let coef_age = 0.1460;

    // Updated renderLatex to include age and fixed education level in the equation
    function renderLatex() {
    const options = { throwOnError: false };
    katex.render(`\\text{Predicted Wage: } Wage = ${intercept.toFixed(2)} + 
    (${coef_educ.toFixed(2)} \\times Education)  + 
    (${coef_race_black.toFixed(2)} \\times Black) + 
    {\\color{red}{(${coef_educ_race_black.toFixed(2)} \\times Education \\times Black)}} + 
    (${coef_age.toFixed(2)} \\times Your Answer)`, document.getElementById('wageBlackEq_AET'), options);

  }

  onMount(() => {
    renderLatex(); // Render your static LaTeX equation once on component mount
  });
</script>

<div class="fontBox">
  <h1 class="fontBox_1">You may question if the variation in education returns is due to unaccounted covariates in the regression analysis.</h1>
  <div class="fontBox_2">
    Let's explore whether the difference in education return persists as we incorporate additional covariates!
  </div>
  <br>
  <div id="wageBlackEq_AET"></div>
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

