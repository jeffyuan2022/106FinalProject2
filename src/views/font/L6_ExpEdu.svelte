<script>
  import { onMount } from 'svelte';

  // Simplified script without the predictive logic and reactive statements

  function renderLatex() {
    const equation = `\\text{Predicted Wage   } Wage = 27.22 + 
    (1.38 \\times Education) + 
    (-3.67 \\times Black) + 
    (-0.24 \\times Education \\times Black) + 
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