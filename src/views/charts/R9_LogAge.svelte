<script>
    import { writable } from 'svelte/store';
    import * as d3 from 'd3';
    import { scaleBand, scaleLinear } from 'd3-scale';
    import { max } from 'd3-array';
  
    let ageLevel = writable(); // Use writable store for age
    let educationLevel = writable(); // Add writable store for education level
    let intercept = 27.2203;
    let coef_educ = 1.3645;
    let coef_race_black = -3.6891;
    let coef_educ_race_black = -0.2486;
    let coef_age = 6.2074;

    let predictedWageWhite, predictedWageBlack;
  
    // Updated function to calculate predicted hourly wage, considering fixed education level
    function predictWageWhite(age, education) {
        let loggedAge = Math.log(age); // This logs the 'age' input.
        return intercept + coef_educ * education + coef_age * loggedAge;
    }
  
    function predictWageBlack(age, education) {
        let loggedAge = Math.log(age); // This logs the 'age' input.
        return intercept + coef_educ * education + coef_race_black + coef_educ_race_black * education + coef_age * loggedAge;
    }

    $: predictedWageWhite = predictWageWhite($ageLevel, $educationLevel);
    $: predictedWageBlack = predictWageBlack($ageLevel, $educationLevel);
  
    // Adjusted for new parameters and fixed education level
    function updateWagesAndDrawChart() {
            drawChart();
    }

    function drawChart() {
        d3.select("#chart_AES").selectAll("*").remove();

    const data = [
      { label: "White", value: predictWageWhite($ageLevel, $educationLevel) },
      { label: "Black", value: predictWageBlack($ageLevel, $educationLevel) }
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
      
      const svg = d3.select("#chart_AES")
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
      .text((d) => `$${d.value.toFixed(2)}`);
  }
  $: {
      if ($ageLevel !== undefined && $educationLevel !== undefined) {
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
  <button on:click={handleCorrectChoice}>log(Age)</button>
  <button on:click={handleWrongChoice}>Age + 5</button>
  {#if showMessage}
  <div>
      <p>Sorry, Pick Again! This can not capture non-linear relationship</p>
  </div>
  {/if}
  
  {#if showContainer}
  <div class=container>
  <div>
    <label for="ageLevel">Age: (Enter a number between 18 - 65)</label>
    <input type="number" bind:value={$ageLevel} min="18" id="ageLevel" placeholder="Enter age here" />
  </div>
  <div>
    <label for="educationLevel">Years of Education:</label>
    <input type="number" bind:value={$educationLevel} min="0" id="educationLevel" placeholder="Enter education years here" />
  </div>
  <br>
   <div class="svg-container_AES">
    <svg id="chart_AES" width="{svgWidth}" height="{svgHeight}"></svg>
    <p class="text">It seems like that the difference in eudcation returns pereisits. </p>
  </div>
  </div>
  {/if}

  <style>
    input, label {
      font-family: Arial, sans-serif;
      margin: 5px 0;
      font-size: 16px;;
    }
    #chart_AES {
      display: block;
      margin: auto;
    }
    .text{
    text-align: center;
    color: red;
    font-weight: bold;
  }
  </style>