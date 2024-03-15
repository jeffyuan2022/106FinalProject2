<script>
      import { onMount } from 'svelte';

      let intercept = 27.2203;
    let coef_educ = 1.3645;
    let coef_race_black = -3.6891;
    let coef_educ_race_black = -0.2486;
    let coef_age = 6.2074;

      function renderLatex() {
      const options = { throwOnError: false };
        katex.render(`\\text{Predicted Wage: } Wage = ${intercept.toFixed(2)} + 
        (${coef_educ.toFixed(2)} \\times Education)  + 
        (${coef_race_black.toFixed(2)} \\times Black) + 
        {\\color{red}{(${coef_educ_race_black.toFixed(2)} \\times Education \\times Black)}} + 
        (${coef_age.toFixed(2)} \\times Your Answer)`, document.getElementById('wageBlackEq_AES'), options);
  
    }
    onMount(async () => {
      renderLatex();
    });

</script>

<div class="fontBox">
    <h1 class="fontBox_1">One might question the complex age-wage relationship, noting that wages don't always rise with age,</h1>
    <div class="fontBox_2">
      contrary to the expected correlation with growing experience.
    </div>
    <br>
    <div id="wageBlackEq_AES"></div>
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