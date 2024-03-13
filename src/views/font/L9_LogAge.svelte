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
  </style>