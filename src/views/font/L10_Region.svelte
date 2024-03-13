<script>
  import { onMount } from 'svelte';

  let coef_age = 0.3027;
    let coef_age_educ = 0.0121;
    let intercept = 33.2258; // Placeholder for intercept from the model
    let coef_educ = 3.6208; // Placeholder for education coefficient from the model
    let coef_race_black = -8.8936; // Placeholder for race (Black) coefficient from the model
    let coef_educ_race_black = -1.7476 ;
    let north = 0.4918;
    let south = -0.5783;
    let west = 0.2919;
    let bnorth = -0.1601;
    let bsouth = 0.3238;
    let bwest = 1.5834;


function renderLatex() {
  const options = { throwOnError: false };
katex.render(`\\text{Predicted Wage: } Wage = ${intercept.toFixed(2)} + 
(${coef_educ.toFixed(2)} \\times Education)  + 
(${coef_race_black.toFixed(2)} \\times Black) + 
{\\color{red}{(${coef_educ_race_black.toFixed(2)} \\times Education \\times Black)}} + 
(${coef_age.toFixed(2)} \\times Age) +
(${north.toFixed(2)} \\times Your Input(?)) +
(${south.toFixed(2)} \\times Your Input(?))+
(${west.toFixed(2)} \\times Your Input(?))+
(${bnorth.toFixed(2)} \\times Your Input(?) \\times Black) +
(${bsouth.toFixed(2)} \\times Your Input(?) \\times Black) +
(${bwest.toFixed(2)} \\times Your Input(?) \\times Black)`, 
document.getElementById('wageBlackEq_AER'), options);
}

onMount(async () => {
      renderLatex();
    });
</script>

<div class="fontBox">
    <h1 class="fontBox_1">But Wait! There's another crucial factor influencing hourly wages that might not be immediately apparent but its impact is significant.Would that change the education return difference?</h1>
    <div id="wageBlackEq_AER"></div>
  </div>

  
  <style>
    .fontBox{
      padding: 20px 0;
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