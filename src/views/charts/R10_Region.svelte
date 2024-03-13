<script>
    import { onMount } from 'svelte';
    import { writable } from 'svelte/store';
    import * as d3 from 'd3';
    import { scaleBand, scaleLinear } from 'd3-scale';
    import { max } from 'd3-array';
    import { base } from '$app/paths';
  
    let ageLevel = writable(18);
    let educationLevel = writable(6); 
    let selectedRegion = writable("Northeast");
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
    
    function getRegionValues(region) {
    // Assuming north, bnorth, south, bsouth, west, and bwest are defined somewhere
    const north = 0.4918; 
    const bnorth = -0.5783;
    const south = 0.2919;
    const bsouth = -0.1601;
    const west = 0.3238;
    const bwest = 1.5834;
    
    if (region === "Northeast") {
        return [north, bnorth];
    } else if (region === "Midwest") {
        return [0, 0];
    } else if (region === "South") {
        return [south, bsouth];
    } else if (region === "West") {
        return [west, bwest];
    } else {
        // Optional: return a default value or throw an error for unrecognized regions
        return [undefined, undefined];
    }
}

    let predictedWageWhite, predictedWageBlack;

    function renderLatex() {
  const options = { throwOnError: false };
  katex.render(`\\text{Predicted Wage: } Wage = ${intercept.toFixed(2)} + 
  (${coef_educ.toFixed(2)} \\times Education)  + 
  (${coef_race_black.toFixed(2)} \\times Black) + 
  {\\color{red}{(${coef_educ_race_black.toFixed(2)} \\times Education \\times Black)}} + 
  (${coef_age.toFixed(2)} \\times Age) +
  (${north.toFixed(2)} \\times North) +
    (${south.toFixed(2)} \\times South)+
    (${west.toFixed(2)} \\times West)+
    (${bnorth.toFixed(2)} \\times North \\times Black) +
    (${bsouth.toFixed(2)} \\times South \\times Black) +
    (${bwest.toFixed(2)} \\times West \\times Black)`, 
  document.getElementById('wageBlackEq_AER'), options);
  }
  
    // Updated function to calculate predicted hourly wage, considering fixed education level
    function predictWageWhite(age, education, region) {
      const [value1, value2] = getRegionValues(region);
      return intercept + coef_educ * education + coef_age * age + coef_age_educ * age * education + value1;
    }
  
    function predictWageBlack(age, education, region) {
      const [value1, value2] = getRegionValues(region);
      return intercept + coef_educ * education + coef_race_black + coef_educ_race_black * education + coef_age * age + coef_age_educ * age * education + value1 + value2;
    }

    $: predictedWageWhite = predictWageWhite($ageLevel, $educationLevel, selectedRegion);
    $: predictedWageBlack = predictWageBlack($ageLevel, $educationLevel, selectedRegion);
  
    // Adjusted for new parameters and fixed education level
    function updateWagesAndDrawChart() {
      renderLatex()
            drawChart();
    }
  
    // Updated renderLatex to include age and fixed education level in the equation

    onMount(async () => {
      drawChart();
    });


    function drawChart() {
        d3.select("#chart_AER").selectAll("*").remove();

    const data = [
      { label: "White", value: predictWageWhite($ageLevel, $educationLevel, selectedRegion) },
      { label: "Black", value: predictWageBlack($ageLevel, $educationLevel, selectedRegion) }
    ];
    // SVG setup
  const svgWidth = 300;
  const svgHeight = 300;
  const margin = {top: 40, right: 30, bottom: 70, left: 60};
  const width = svgWidth - margin.left - margin.right;
  const height = svgHeight - margin.top - margin.bottom;

    const x = scaleBand()
      .range([0, width])
      .domain(data.map((d) => d.label))
      .padding(0.1);
      
    const y = scaleLinear()
        .domain([0, max(data, (d) => d.value)])
        .range([height, 0]);
      
      const svg = d3.select("#chart_AER")
                .attr("width", svgWidth)
                .attr("height", svgHeight)
                .append("g")
                .attr("transform", `translate(${margin.left},${margin.top})`);

     // Add x-axis
    svg.append("g")
       .attr("transform", "translate(0," + height + ")")
       .call(d3.axisBottom(x));

    // Add y-axis
    svg.append("g")
       .call(d3.axisLeft(y));

       svg.append("text")
  .attr("transform", "rotate(-90)")
  .attr("y", 0 - margin.left)
  .attr("x",0 - (height / 2))
  .attr("dy", "1em")
  .style("text-anchor", "middle")
  .text("Predicted Wage");
    
    svg.selectAll(".bar")
      .data(data)
      .join("rect")
      .attr("class", "bar")
      .attr("x", (d) => x(d.label))
      .attr("width", x.bandwidth())
      .attr("y", (d) => y(d.value))
      .attr("height", (d) => height - y(d.value))
      .attr("fill", (d) => d.label === "White" ? "steelblue" : "red");
      
    svg.selectAll(".label")
      .data(data)
      .join("text")
      .attr("class", "label")
      .attr("x", (d) => x(d.label) + x.bandwidth() / 2)
      .attr("y", (d) => y(d.value) - 5)
      .attr("text-anchor", "middle")
      .text((d) => d.value.toFixed(2));
  }
  $: {
      if ($ageLevel !== undefined && $educationLevel !== undefined && selectedRegion !== undefined) {
        updateWagesAndDrawChart();
      }
    }
    let showContainer = false;
  let showMessage = false;

  // Assuming dimensions for the SVG for demonstration purposes
  const svgWidth = 600; // Width of your SVG container
  const svgHeight = 400; // Height of your SVG container

  function handleCorrectChoice() {
    showContainer = true;
    showMessage = false;
  }

  function handleWrongChoice() {
    showContainer = false;
    showMessage = true;
  }
  </script>

<p>Please click one of the options below that you think could be a possible statistically significant covariate when predicting hourly wages:</p>
<button on:click={handleCorrectChoice}>Region</button>
<button on:click={handleWrongChoice}>Favorite Color</button>
{#if showMessage}
<div>
    <p>An individual's favorite color is an example of a variable that has no direct impact on hourly wage. Favorite color is a personal preference and lacks any economic or labor market relevance.</p>
</div>
{/if}

{#if showContainer}
<div class=container>
        <div>
        <label for="ageLevel">Age:</label>
        <input type="number" bind:value={$ageLevel} min="18" id="ageLevel" placeholder="Enter age here" />
      </div>
      <div>
        <label for="educationLevel">Years of Education:</label>
        <input type="number" bind:value={$educationLevel} min="0" id="educationLevel" placeholder="Enter education years here" />
      </div>
      <div>
        <label for="region-select">Choose a Region:</label>
        <select bind:value={selectedRegion} id="region-select">
            <option value="">--Please choose an option--</option>
            <option value="Northeast">Northeast</option>
            <option value="Midwest">Midwest</option>
            <option value="South">South</option>
            <option value="West">West</option>
        </select>
      </div> <div class="svg-container_AER">
        <svg id="chart_AER"></svg>
        <p class="text">It seems like that the difference in eudcation returns pereisits. </p>
        <div id="wageBlackEq_AER"></div>
      </div>
</div>
{/if}
  
  <style>
  input, select, label {
    margin: 5px 0;
    font-size: 18px;
  }
  #chart_AER {
    font-family: Arial, sans-serif;
    display: block;
    margin: auto;
  }
  .text{
    text-align: center;
    color: red;
    font-weight: bold;
  }
  </style>