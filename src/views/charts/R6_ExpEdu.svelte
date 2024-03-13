<script>
  import { onMount } from 'svelte';
  import { writable } from 'svelte/store';
  import * as d3 from 'd3';

  let intercept = 27.2222; // Placeholder for intercept from the model
  let coef_educ = 1.4159; // Placeholder for education coefficient from the model
  let coef_race_black = -3.7059; // Placeholder for race (Black) coefficient from the model
  let coef_educ_race_black = -0.2296;

  $: predictedWageWhite = $educationLevel * coef_educ + intercept;
  $: predictedWageBlack = ($educationLevel * coef_educ + intercept) + (coef_race_black) + ($educationLevel * coef_educ_race_black);

  onMount(async () => {
    drawCombinedGraph();
  });
  ///////
  let educationLevel = writable();

  // Function to calculate predicted hourly wage for White individuals
  function predictWageWhite(education) {
    return intercept + coef_educ * education;
  }

  // Function to calculate predicted hourly wage for Black individuals
  function predictWageBlack(education) {
    return intercept + coef_educ * education + coef_race_black + coef_educ_race_black * education;
  }
  $: $educationLevel, drawCombinedGraph();
  
  function drawCombinedGraph() {
  // Clear existing graph to prevent overlap
  d3.select("#chart").selectAll("*").remove();

  // SVG setup
  const svgWidth = 500;
  const svgHeight = 450;
  const margin = {top: 40, right: 30, bottom: 70, left: 60};
  const width = svgWidth - margin.left - margin.right;
  const height = svgHeight - margin.top - margin.bottom;

  // Append SVG object to the body of the page
  const svg = d3.select("#chart")
                .attr("width", svgWidth)
                .attr("height", svgHeight)
                .append("g")
                .attr("transform", `translate(${margin.left},${margin.top})`);

  // Prepare the data
  const data = [{
    education: "White",
    wage: predictWageWhite($educationLevel)
  }, {
    education: "Black",
    wage: predictWageBlack($educationLevel)
  }];

  // X Axis
  const x = d3.scaleBand()
    .range([0, width])
    .domain(data.map(d => d.education))
    .padding(0.1);
  
  svg.append("g")
    .attr("transform", `translate(0, ${height})`)
    .call(d3.axisBottom(x));

  // Y Axis
  const y = d3.scaleLinear()
    .domain([0, d3.max(data, d => d.wage)])
    .range([height, 0]);
  
  svg.append("g")
    .call(d3.axisLeft(y));
  
  svg.append("text")
  .attr("transform", "rotate(-90)")
  .attr("y", 0 - margin.left)
  .attr("x",0 - (height / 2))
  .attr("dy", "1em")
  .style("text-anchor", "middle")
  .text("Predicted Wage");

  // Bars
  svg.selectAll(".bar")
    .data(data)
    .enter().append("rect")
      .attr("class", "bar")
      .attr("x", d => x(d.education))
      .attr("width", x.bandwidth())
      .attr("y", d => y(d.wage))
      .attr("height", d => height - y(d.wage))
      .attr("fill", d => d.education === "White" ? "steelblue" : "red");

      svg.selectAll(".label")
      .data(data)
      .join("text")
      .attr("class", "label")
      .attr("x", (d) => x(d.education) + x.bandwidth() / 2)
      .attr("y", (d) => y(d.wage) - 5)
      .attr("text-anchor", "middle")
      .text((d) => d.wage.toFixed(2));



}
</script>

<div>
  <h2>Education Level Input</h2>
  <label for="educationLevel">Years of Education:</label>
  <input type="number" bind:value={$educationLevel} min="0" id="educationLevel" placeholder="Change the years of education here" />
</div>
<div class="svg-container">
  <svg id="chart"></svg>
</div>
  
  <style>
    .box{
      width: 100%;
      height: 100%;
      padding: 20px 0;
    }
    #chart-container-line-1{
      width: 100%;
      height: 100%;
    }
    input, label {
    font-family: Arial, sans-serif;
    margin: 5px 0;
    font-size: 24px;;
  }

  #chart {
  display: block;
  margin: auto;
}
  </style>
  